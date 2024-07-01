# kf-final-task
Final task of project based internship by Kimia Farma

SELECT kft.transaction_id, kft.date, kft.branch_id, kkc.branch_name, kkc.kota, kkc.provinsi, kkc.rating as rating_cabang, kft.customer_name, ki.product_id, ki.product_name, kp.price as actual_price, kft.discount_percentage, 
CASE WHEN kp.price <= 50000 THEN 0.1 
ELSE 
CASE WHEN kp.price> 50000 AND kp.price < 100000 THEN 0.15 
ELSE
CASE WHEN kp.price >= 100000 AND kp.price < 300000 THEN 0.2 
ELSE
CASE WHEN kp.price >= 300000 AND kp.price < 500000 THEN 0.25 
ELSE 0.3 
END END END END 
as persentase_gross_laba, 
kft.discount_percentage * kft.price as nett_sales, 
kft.price * CASE WHEN kp.price <= 50000 THEN 0.1  ELSE 
CASE WHEN kp.price> 50000 AND kp.price < 100000 THEN 0.15 
ELSE
CASE WHEN kp.price >= 100000 AND kp.price < 300000 THEN 0.2 
ELSE
CASE WHEN kp.price >= 300000 AND kp.price < 500000 THEN 0.25 
ELSE 0.3 
END END END END as nett_profit,
kft.rating as rating_transaksi 
FROM `magnetic-tenure-427916-b6.kimia_farma.kf_final_transaction` kft
LEFT JOIN `magnetic-tenure-427916-b6.kimia_farma.kf_inventory` ki
ON kft.branch_id = ki.branch_id
LEFT JOIN `magnetic-tenure-427916-b6.kimia_farma.kf_kantor_cabang` kkc
ON ki.branch_id = kkc.branch_id
LEFT JOIN `magnetic-tenure-427916-b6.kimia_farma.kf_product` kp
ON kp.product_id = ki.product_id AND kp.product_name = ki.product_name 

LIMIT 1000
