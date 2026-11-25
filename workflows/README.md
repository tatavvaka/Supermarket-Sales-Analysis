# Orange Workflow Notes

`analisis-prediktif-supermarket.ows` merupakan workflow Orange Data Mining yang disediakan bersama project.

Workflow mencakup widget File, Select Columns, Data Sampler, Preprocess, Linear Regression, Random Forest, Test and Score, Predictions, dan Data Table.

Deskripsi workflow mencatat target pemodelan, delapan input features, pembagian data 80/20, evaluation metrics, selected prediction examples, dan limitations. Ringkasan tersedia pada [Model Evaluation Notes](../docs/model-evaluation.md).

**Portability note:** File widget pada workflow asli menyimpan local Windows path ke workbook sumber. Saat dibuka di komputer lain atau setelah workbook dipindahkan, Orange mungkin meminta lokasi file ditentukan ulang. File workflow dipertahankan tanpa mengubah pengaturan internalnya.
