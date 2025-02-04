<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Martabak TOP Jakarta</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #f8b400;
            color: white;
            padding: 20px;
            text-align: center;
        }
        nav {
            background-color: #333;
            padding: 10px;
            text-align: center;
        }
        nav a {
            color: white;
            margin: 0 15px;
            text-decoration: none;
            font-weight: bold;
        }
        nav a:hover {
            text-decoration: underline;
        }
        section {
            padding: 20px;
            margin: 20px auto;
            max-width: 800px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        footer {
            background-color: #f8b400;
            color: white;
            text-align: center;
            padding: 10px;
            position: fixed;
            bottom: 0;
            width: 100%;
        }
        form input, form select {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            box-sizing: border-box;
        }
        form input[type="submit"] {
            background-color: #f8b400;
            color: white;
            border: none;
            cursor: pointer;
        }
        form input[type="submit"]:hover {
            background-color: #333;
        }
        .order-summary {
            margin-top: 20px;
            padding: 20px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
        }
        .price-table img {
            width: 100%;
            max-width: 800px;
        }
    </style>
    <script>
        const prices = {
            "original": {
                "biasa": {"polos": 18000, "kacang": 20000, "coklat": 20000, "pisang": 20000, "kismis": 20000, "keju": 20000, "pisang coklat": 25000, "kacang coklat": 25000, "keju coklat": 25000, "keju pisang": 25000, "keju kismis": 25000, "keju coklat kacang": 30000, "keju ½ coklat kacang": 30000, "keju kismis campur": 30000, "keju pisang campur": 33000},
                "spesial": {"kacang": 25000, "coklat": 25000, "pisang": 25000, "kismis": 25000, "keju": 25000, "pisang coklat": 28000, "kacang coklat": 28000, "keju coklat": 30000, "keju pisang": 30000, "keju kismis": 30000, "keju coklat kacang": 33000, "keju ½ coklat kacang": 33000, "keju kismis campur": 35000, "keju pisang campur": 35000}
            },
            "pandan": {
                "biasa": {"polos": 20000, "kacang": 25000, "coklat": 25000, "pisang": 25000, "kismis": 25000, "keju": 25000, "pisang coklat": 28000, "kacang coklat": 28000, "keju coklat": 30000, "keju pisang": 30000, "keju kismis": 30000, "keju coklat kacang": 33000, "keju ½ coklat kacang": 33000, "keju kismis campur": 35000, "keju pisang campur": 35000},
                "spesial": {"kacang": 28000, "coklat": 28000, "pisang": 28000, "kismis": 28000, "keju": 28000, "pisang coklat": 30000, "kacang coklat": 30000, "keju coklat": 33000, "keju pisang": 33000, "keju kismis": 33000, "keju coklat kacang": 35000, "keju ½ coklat kacang": 35000, "keju kismis campur": 38000, "keju pisang campur": 38000}
            },
            "black sweet": {
                "biasa": {"polos": 20000, "kacang": 25000, "coklat": 25000, "pisang": 25000, "kismis": 25000, "keju": 25000, "pisang coklat": 28000, "kacang coklat": 28000, "keju coklat": 30000, "keju pisang": 30000, "keju kismis": 30000, "keju coklat kacang": 33000, "keju ½ coklat kacang": 33000, "keju kismis campur": 35000, "keju pisang campur": 35000},
                "spesial": {"kacang": 28000, "coklat": 28000, "pisang": 28000, "kismis": 28000, "keju": 28000, "pisang coklat": 30000, "kacang coklat": 30000, "keju coklat": 33000, "keju pisang": 33000, "keju kismis": 33000, "keju coklat kacang": 35000, "keju ½ coklat kacang": 35000, "keju kismis campur": 38000, "keju pisang campur": 38000}
            },
            "telor": {
                "biasa": {"ayam": 25000, "sapi": 28000, "kombinasi": 30000},
                "spesial": {"ayam": 30000, "sapi": 33000, "kombinasi": 35000},
                "super": {"ayam": 35000, "sapi": 40000, "kombinasi": 40000}
            }
        };

        function displayOrderSummary(event) {
            event.preventDefault();
            const name = document.getElementById('name').value;
            const address = document.getElementById('address').value;
            const product = document.getElementById('product').value;
            const type = document.querySelector('input[name="type"]:checked').value;
            const variant = document.getElementById('variant').value;
            const quantity = document.getElementById('quantity').value;

            const productName = product.charAt(0).toUpperCase() + product.slice(1);
            const totalPrice = prices[product][type][variant] * quantity;

            const orderSummary = `
                <h3>Order Summary</h3>
                <p><strong>Nama:</strong> ${name}</p>
                <p><strong>Alamat:</strong> ${address}</p>
                <p><strong>Produk:</strong> ${productName}</p>
                <p><strong>Tipe:</strong> ${type.charAt(0).toUpperCase() + type.slice(1)}</p>
                <p><strong>Varian:</strong> ${variant.charAt(0).toUpperCase() + variant.slice(1)}</p>
                <p><strong>Jumlah:</strong> ${quantity}</p>
                <p><strong>Total Harga:</strong> Rp ${totalPrice.toLocaleString('id-ID')}</p>
            `;

            document.getElementById('order-summary').innerHTML = orderSummary;
        }
    </script>
</head>
<body>
    <header>
        <h1>Martabak TOP Jakarta</h1>
        <p><i>Khas Pecenongan</i></p>
    </header>
    <nav>
        <a href="#home">Home</a>
        <a href="#produk">Produk</a>
        <a href="#order">Order Online</a>
        <a href="#blog">Blog</a>
        <a href="#tentang">Tentang Kami</a>
        <a href="#kontak">Kontak</a>
    </nav>
    <section id="home">
        <h2>Selamat Datang di Martabak TOP Jakarta</h2>
        <p>Martabak lezat dan nikmat langsung diantarkan ke rumah Anda.</p>
    </section>
    <section id="produk">
        <h2>Produk Kami</h2>
        <h3>Martabak Manis</h3>
        <p>Berbagai pilihan topping yang menggugah selera.</p>
        <h3>Martabak Telur</h3>
        <p>Martabak telur dengan isian daging yang melimpah.</p>
        <img src ="daftar harga.png" width="550px" height="400px" alt="Martabak">
    </section>
    <section id="order">
        <h2>Order Online</h2>
        <form onsubmit="displayOrderSummary(event)">
            <label for="name">Nama:</label>
            <input type="text" id="name" name="name" required>
            <label for="address">Alamat:</label>
            <input type="text" id="address" name="address" required>
            <label for="product">Pilih Produk:</label>
            <select id="product" name="product">
                <option value="original">Martabak Original</option>
                <option value="pandan">Martabak Pandan</option>
                <option value="black sweet">Martabak Black Sweet</option>
                <option value="telor">Martabak Telor</option>
            </select>
            <label>Tipe:</label>
            <input type="radio" id="biasa" name="type" value="biasa" checked>
            <label for="biasa">Biasa</label>
            <input type="radio" id="spesial" name="type" value="spesial">
            <label for="spesial">Spesial</label>
            <input type="radio" id="super" name="type" value="super">
            <label for="super">Super</label>
            <label for="variant">Pilih Varian:</label>
            <select id="variant" name="variant">
                <option value="polos">Polos</option>
                <option value="kacang">Kacang</option>
                <option value="coklat">Coklat</option>
                <option value="pisang">Pisang</option>
                <option value="kismis">Kismis</option>
                <option value="keju">Keju</option>
                <option value="pisang coklat">Pisang Coklat</option>
                <option value="kacang coklat">Kacang Coklat</option>
                <option value="keju coklat">Keju Coklat</option>
                <option value="keju pisang">Keju Pisang</option>
                <option value="keju kismis">Keju Kismis</option>
                <option value="keju coklat kacang">Keju Coklat Kacang</option>
                <option value="keju ½ coklat kacang">Keju ½ Coklat Kacang</option>
                <option value="keju kismis campur">Keju Kismis Campur</option>
                <option value="keju pisang campur">Keju Pisang Campur</option>
                <option value="ayam">Ayam</option>
                <option value="sapi">Sapi</option>
                <option value="kombinasi">Kombinasi</option>
            </select>
            <label for="quantity">Jumlah:</label>
            <input type="number" id="quantity" name="quantity" required>
            <input type="submit" value="Order">
        </form>
        <div id="order-summary" class="order-summary"></div>
    </section>
    <section id="blog">
        <h2>Blog</h2>
        <article>
            <h3>Toko Offline khusus Bandung</h3>
            <ul>
                <li>Jl. Terusan Jakarta</li>
                <li>Jl. Cinambo</li>
                <li>Jl. Sindanglaya</li>
            </ul>
        </article>
        <article>
            <h3>Terima Kasih Sudah Membeli Martabak TOP Jakarta</h3>
        </article>
    </section>
    <section id="tentang">
        <h2>Tentang Kami</h2>
        <p>Nama: Devarian Firmansyah</p>
        <p>Kelas: IS-3</p>
        <img src="gambarHTML.png" width="200px" height="200px" alt="Devarian Firmansyah">
    </section>
    <section id="kontak">
        <h2>Kontak</h2>
        <p>Hubungi kami di:</p>
        <p>Email: devarian.10523094@mahasiswa.unikom.ac.id</p>
        <p>NIM: 10523094</p>
    </section>
    <footer>
        <p>&copy; Martabak TOP Jakarta. All rights reserved.</p>
    </footer>
</body>
</html>
