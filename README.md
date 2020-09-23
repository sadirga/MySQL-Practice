# MySQL-Practice
Practice-Assignment of MySQL

[![logopwdk.png](https://i.postimg.cc/66VC3Rgx/logopwdk.png)](https://postimg.cc/s1XMHB3T)




#

### **Cinematic Universe**

MySQL secara default menyertakan database ```sakila``` yang dapat digunakan oleh user untuk mempelajari teknik penggunaan database di MySQL. Database ```sakila``` merupakan sample dummy database yang menyimpan informasi seputar toko rental DVD.

*__Soal :__* Aktifkan server MySQL Anda, lalu gunakan database ```sakila``` dan tuliskan langkah-langkah/query MySQL untuk menyelesaikan perintah berikut. Anda dilarang membuat database baru, merubah struktur table, membuat view atau segala bentuk tindakan yang mengubah struktur database.

1. Tampilkan daftar __10 film komedi dengan durasi tersingkat__. Urutkan data berdasarkan film dengan durasi terpendek. Kolom yang diwajibkan tampil adalah __title__, __category__ dan __length__. Output yang diharapkan:

    ## Query
    ```bash
    SELECT title,name as 'Category',length FROM Film,Category,film_category
    WHERE Film.film_id = film_category.film_id and category.category_id = film_category.category_id and name='Comedy' ORDER BY length LIMIT 10;
    ```
      
    > [![NO1.png](https://i.postimg.cc/Gh5n6crb/NO1.png)](https://postimg.cc/MvVLQJvL)
    
    
2. Tampilkan daftar lengkap __kategori film beserta jumlah film tiap kategori & rata-rata harga sewa DVD film tiap kategori__. Urutkan data dari kategori dengan jumlah film terbanyak. Kolom yang diwajibkan ada minimal adalah __kategori__, __jumlah film__ dan __rata-rata harga sewa__. Output yang diharapkan:

    ## Query
    ```bash
    SELECT name as 'kategori', count(title) as 'jumlahMovie',Avg(rental_rate) as 'rataHargaSewa' FROM film,film_category,category 
    -> WHERE Film.film_id = film_category.film_id and category.category_id = film_category.category_id GROUP BY name ORDER BY jumlahMovie DESC;
    ```
    
    > [![no2.png](https://i.postimg.cc/52K5wRw7/no2.png)](https://postimg.cc/21vBYT9h)
    
3. [Motion Picture Association of America](https://en.wikipedia.org/wiki/Motion_Picture_Association_of_America_film_rating_system) memiliki sistem rating untuk film berdasarkan konten & target penontonnya dengan klasifikasi sebagai berikut:

    - **G** : General Audiences
    - **PG** : Parental Guidance Suggested
    - **PG-13** : Parental Guidances for Children Under 13
    - **R** : Restricted
    - **NC-17** : No Children Under 17 Admitted

    Tampilkan daftar lengkap __rating film beserta keterangan arti rating & jumlah film tiap rating__. Kolom yang diwajibkan ada minimal adalah __rating__, __keterangan rating__ dan __jumlah film__. Output yang diharapkan:

    ## Query
    ```bash
    SELECT rating, CASE WHEN rating = 'G' THEN 'General Audiences'
    -> WHEN rating = 'PG' THEN 'Parental Guidance Suggested'
    -> WHEN rating = 'PG-13' THEN 'Parental Guidances for Under 13'
    -> WHEN rating = 'R' THEN 'Restricted'
    -> WHEN rating = 'NC-17' THEN 'No Children Under 17 Admitted' END AS Keterangan, count(title) as 'jumlahMovie' from film GROUP BY rating ORDER BY rating;
    ```
    > [![NO-3.png](https://i.postimg.cc/B6BXCjrS/NO-3.png)](https://postimg.cc/Fd1rrHF8)

4. Tampilkan daftar __10 aktor/aktris yang paling banyak membintangi film__. Kolom yang ditampilkan minimal: __id aktor__, __nama depan__, __nama belakang__ dan __jumlah film yang dibintangi__ kemudian urutkan dari aktor/aktris yang membintangi film terbanyak. Output yang diharapkan:

    ## Query
    ```bash
    SELECT actor_id,first_name,last_name,(SELECT count(film_id) FROM film_actor fa WHERE fa.actor_id = a.actor_id) as jumlah_movie
    -> FROM actor_info a ORDER BY jumlah_movie DESC LIMIT 10;
    ```
    
    > [![no4.png](https://i.postimg.cc/W4M32DbG/no4.png)](https://postimg.cc/QBdsmd7C)
    
5. Dari soal sebelumnya diketahui ```Gina Degeneres``` merupakan aktris yang paling banyak membintangi film, dengan total **42** judul film. Kategori film apakah yang paling banyak dibintanginya? Untuk mengetahuinya, tampilkan daftar __kategori film beserta jumlah film yang pernah dibintangi oleh ```Gina Degeneres```__. Kolom yang diwajibkan ada yaitu __kategori film__ dan __jumlah film yang dibintangi__. Output yang diharapkan:

    ## Query
    ```bash
    SELECT Category, count(*) as 'jumlahMovie' FROM film_list WHERE actors LIKE '%GINA%' GROUP BY Category;
    ```
    
    > [![NO5.png](https://i.postimg.cc/MT5pQhBX/NO5.png)](https://postimg.cc/DJWhVpBK)
  
6. Dari soal sebelumnya diketahui ```Gina Degeneres``` paling banyak membintangi film bergenre science-fiction, dengan total **7** judul film. Tampilkan daftar __judul film sci-fi yang pernah dibintangi oleh ```Gina Degeneres```__. Kolom yang diwajibkan ada yaitu __judul film__ dan __kategorinya__. Output yang diharapkan:

    ## Query
    ```bash
     SELECT title, category FROM film_list WHERE actors LIKE '%GINA%' AND category='Sci-Fi' GROUP BY Title;
     ```
     
    > [![no6.png](https://i.postimg.cc/BbvQcM5p/no6.png)](https://postimg.cc/2bPDCdKL)
  
7. Tampilkan daftar __10 aktor/aktris yang paling banyak membintangi film horror__. Kolom yang ditampilkan minimal: __id aktor__, __nama depan__, __nama belakang__ dan __jumlah film horror yang dibintangi__ kemudian urutkan dari aktor/aktris yang membintangi film horror terbanyak. Output yang diharapkan:

    ## Query
    ```bash
    SELECT A.actor_id, A.first_name, A.last_name, count(title) as jumlah_movie FROM actor A, film_list fl, film_actor fa
    -> WHERE A.actor_id = fa.actor_id AND fl.FID = fa.film_id AND category='horror' GROUP BY fa.actor_id ORDER BY jumlah_movie DESC LIMIT 10;
    ```
    
    > [![NO7.png](https://i.postimg.cc/Dy8wSpwy/NO7.png)](https://postimg.cc/RNxB8Rtj)
    
8. Dari soal sebelumnya diketahui ```Julia McQueen``` merupakan aktris yang paling banyak membintangi film horror, dengan total **7** judul film. Tampilkan daftar __judul film horror yang pernah dibintangi oleh ```Julia McQueen```__. Kolom yang diwajibkan ada yaitu __judul film__ dan __kategorinya__. Output yang diharapkan:

    ## Query
    ```bash
    SELECT title, category from film_list WHERE actors LIKE '%Julia Mc%' AND category ='horror';
    ```
    
    > [![no8.png](https://i.postimg.cc/c4gdxKFv/no8.png)](https://postimg.cc/3dTs9w5h)
