# Data Dictionary

Worksheet utama: `sources` dengan 10,076 rows dan 24 columns. Terdapat 21 original fields dan tiga prepared fields. Kolom sumber tetap dipertahankan agar proses preparation dapat ditelusuri.

| Column | Meaning | Notes |
|---|---|---|
| `row_id` | Identifier-like field | Tidak unik pada export; jangan gunakan sebagai primary key tanpa validasi. |
| `order_id` | Order identifier | Satu pesanan dapat memiliki beberapa transaction lines. |
| `tanggal_pemesanan` | Order date | Dasar analisis periode 2014–2017. |
| `tanggal_pengiriman` | Original shipping date | Memiliki missing values pada source. |
| `metode_pengiriman` | Shipping method | Standard Class, Second Class, First Class, Same Day. |
| `customer_id` | Customer identifier | Identifier sintetis. |
| `nama_pelanggan` | Customer name | Field nama sintetis; tidak digunakan sebagai model feature. |
| `segmen` | Customer segment | Consumer, Corporate, Home Office. |
| `negara` | Country | Indonesia pada dataset yang diberikan. |
| `kota` | Original city | Memiliki missing values dan variasi kapitalisasi. |
| `provinsi` | Province | Provinsi yang terkait dengan transaksi. |
| `kode_pos` | Original postal code | Memiliki missing values. |
| `wilayah` | Sales region | Central, East, South, West. |
| `product_id` | Product identifier | Identifier produk sintetis. |
| `kategori` | Product category | Furniture, Office Supplies, Technology. |
| `sub_kategori` | Product subcategory | Label subkategori produk. |
| `nama_produk` | Product name | Nama produk sintetis. |
| `penjualan` | Sales amount | Nilai penjualan per transaction line dalam IDR. |
| `kuantitas` | Quantity | Unit pada transaction line. |
| `diskon` | Discount | Discount rate sebagaimana tersimpan di source. |
| `keuntungan` | Profit | Profit per transaction line dalam IDR; nilai negatif dipertahankan. |
| `clean_tanggal_pengiriman` | Prepared shipping date | Missing value diisi dengan order date; hasil imputasi merupakan asumsi. |
| `clean_kota` | Prepared city | Kota dimapping dari provinsi ketika kosong, lalu distandardisasi. |
| `clean_kode_pos` | Prepared postal code | Kode pos lima digit yang dimapping dari provinsi ketika kosong. |

