# Fundamental SQL Group By and Having

## Fungsi Having
HAVING digunakan untuk menggantikan WHERE ketika menggunakan Group BY 
yang datanya di aggregasi.
Secara umum HAVING digunakan setelah melakukan GROUP BY berikut sintaks yang digunakan:

    SELECT nama_kolom
    FROM nama_table
    GROUP BY nama_kolom
    HAVING kondisi
    
## Contoh penggunaan HAVING
Syntax:

    SELECT customer_id FROM Subscription 
    GROUP BY customer_id 
    HAVING COUNT(customer_id) > 1;
    
Output:

![image](https://user-images.githubusercontent.com/110078907/213624043-20c797fb-4d7c-4f0a-84b3-67068bf84e6c.png)

## Menampilkan Konsumen yang berubah berlangganan
Contoh:
1. customer_id
2. product_id
3. subscription_date

Syntax:

    SELECT customer_id, product_id, subscription_date
    FROM Subscription 
    WHERE customer_id IN 
       (
       SELECT customer_id 
       FROM Subscription 
       GROUP BY customer_id 
       HAVING COUNT(customer_id) > 1
       ) 
    ORDER BY customer_id ASC;

Output:

![image](https://user-images.githubusercontent.com/110078907/213625156-f5fb4456-d5a9-4a1d-a805-3ca73ddd7d70.png)

## Menampilkan detail konsumen
Contoh JOIN table subscription dan customer dengan menggabungkan
customer_id dari table subscription dan id dari table customer
Syntax:

    SELECT b.name, b.address, b.phone, a.product_id, a.subscription_date 
    FROM Subscription a 
    JOIN customer b ON a.customer_id=b.id 
        WHERE b.id IN 
        (
        SELECT customer_id 
        FROM Subscription 
        GROUP BY customer_id 
        HAVING COUNT(customer_id) > 1
        ) 
    ORDER BY b.id ASC;

Output:

![image](https://user-images.githubusercontent.com/110078907/213626203-d5c42eca-bc0d-49b0-a2ec-6f133d7f2817.png)

## Fungsi MAX pada Having
Syntax:

    select product_id, max(total_price) as total 
    from invoice 
    group by product_id;
    select product_id, max(total_price) as total 
    from invoice 
    group by product_id having max(total_price) > 1000000;
    select product_id, max(pinalty) as total 
    from invoice 
    group by product_id having max(pinalty) > 30000;

Output:

![image](https://user-images.githubusercontent.com/110078907/213626780-6508f66f-c86f-4763-8a1f-3fbe75f2cb76.png)

## Fungsi MIN pada Having
Syntax:

    select product_id, min(total_price) as total 
    from invoice 
    group by product_id;
    select product_id, min(total_price) as total 
    from invoice 
    group by product_id having min(total_price) < 500000;
    select product_id, min(pinalty) as total 
    from invoice 
    group by product_id having min(pinalty) < 50000;

Output:

![image](https://user-images.githubusercontent.com/110078907/213627513-20868ad1-7e1c-4fff-9c1b-af153c082bb7.png)

## Fungsi AVG di Having
Syntax:

    select product_id, avg(total_price) as total 
    from invoice 
    group by product_id;
    select product_id, avg(total_price) as total 
    from invoice 
    group by product_id having avg(total_price) > 100000;
    select product_id, avg(pinalty) as total 
    from invoice 
    group by product_id having avg(pinalty) > 30000;

Output: 

![image](https://user-images.githubusercontent.com/110078907/213628126-723276ba-988b-4d67-b72b-13856eab670c.png)

## Contoh Mini Project
Lakukan query untuk dapat mengeluarkan product_id, rata-rata nilai pinalty dan jumlah customer_id yang di group by berdasarkan product_id
yang memiliki jumlah customer_id diatas nilai 20.
Syntax:

    SELECT product_id, AVG(pinalty),
    COUNT(customer_id) AS total 
    FROM invoice 
    GROUP BY product_id 
    HAVING COUNT(customer_id) > 20;
    
Output:

![image](https://user-images.githubusercontent.com/110078907/213628569-6c46f2f7-871d-4c6c-ab64-91540d901508.png)

## Kesimpulan yang bisa didapatkan adalah:
1. Menggunakan fungsi SELECT untuk menampilkan data-data yang butuh diketahui informasinya. 
2. Menggunakan fungsi Group by dan Join untuk memahami penggunaan Having.
3. Menghitung nilai Max, Min dan Avg pada penerapan fungsi Having. 
