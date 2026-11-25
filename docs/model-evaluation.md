# Predictive Modeling Notes — Profit Estimation

## Modeling objective

Mengestimasi `keuntungan` (profit) untuk setiap transaction line. Ini adalah regression task, bukan time-series forecast.

## Workflow design recorded in the Orange `.ows` file

- Dataset: 10,076 transaction rows from the cleaned `sources` worksheet.
- Target: `keuntungan`.
- Numeric features: `penjualan`, `kuantitas`, `diskon`.
- Categorical features: `kategori`, `sub_kategori`, `segmen`, `metode_pengiriman`, `clean_kota`.
- Metadata: `row_id`, `order_id`, `nama_produk`.
- Split: 80% training (8,061 rows) and 20% testing (2,015 rows), with deterministic sampling.
- Learners: Linear Regression and Random Forest.
- Evaluation: Test on test data.

## Recorded performance scores

| Model | RMSE (IDR) | MAE (IDR) | R² |
|---|---:|---:|---:|
| Linear Regression | 3,232,527.847 | 916,608.092 | 0.191 |
| Random Forest | 2,019,690.066 | 298,859.767 | 0.684 |

Scores ditranskripsikan dari deskripsi yang tertanam pada supplied Orange workflow. Workflow belum direproduksi melalui eksekusi ulang pada tahap dokumentasi ini.

## Interpretation

Random Forest performs better than Linear Regression on the recorded test split: RMSE and MAE are lower, while R² is higher. R² merupakan coefficient of determination, bukan accuracy percentage. Selisih RMSE dan MAE mengindikasikan sebagian prediksi memiliki error yang relatif besar. MAPE tercatat sebagai infinite (`inf`) pada kedua model dan tidak digunakan sebagai pembanding.

## Selected prediction examples

| row_id | Actual profit (IDR) | Linear Regression (IDR) | Random Forest (IDR) |
|---:|---:|---:|---:|
| 4947 | 26,814.00 | 558,527.80 | 13,320.20 |
| 9624 | -818,244.00 | -2,508,885.90 | -788,307.20 |
| 9933 | 202,230.00 | 343,722.10 | 204,544.60 |

Contoh ini menunjukkan beberapa prediksi pada test set yang sama. Perbandingan model tetap didasarkan pada keseluruhan 2,015 testing rows, bukan hanya tiga contoh tersebut.

## Limitations

- Dataset bersifat sintetis.
- Evaluasi menggunakan satu deterministic random row-level split.
- Rows dari order yang sama dapat tersebar pada training dan testing; performa pada entirely unseen orders atau customers belum terbukti.
- Model mengestimasi profit per transaction line, bukan future sales atau total store profit.
- Deskripsi workflow tidak mencatat time-based validation atau repeated cross-validation.
- Skor belum diverifikasi ulang melalui eksekusi workflow pada mesin yang berbeda.
