# Postest_2
Muhammad Danil Pratama (2309116091)
# Data produk awal
produk = [
    {"id": 1, "nama": "Hoodie", "harga": 255000, "stok": 18},
    {"id": 2, "nama": "Baju Kaos", "harga": 99999, "stok": 32},
    {"id": 3, "nama": "Celana formal", "harga": 125000, "stok": 15},
    {"id": 4, "nama": "Sepatu", "harga": 220000, "stok": 10}

# Fungsi untuk menampilkan produk dalam bentuk tabel
def tampilkan_produk():
    table = PrettyTable()
    table.field_names = ["ID", "Nama", "Harga (Rp.)", "Stok"]
    for product in produk:
        table.add_row([product["id"], product["nama"], locale.currency(product['harga'], grouping=True), product["stok"]])
    print(table)

   # Fungsi untuk menambah produk (hanya admin)
def tambah_produk():
    if not is_admin():
        print("Anda tidak memiliki izin untuk menambah produk.")
        return

    nama = input("Masukkan nama produk: ")
    harga = int(input("Masukkan harga produk (dalam Rp.): "))
    stok = int(input("Masukkan stok produk: "))

    produk_id = len(produk) + 1
    produk_baru = {"id": produk_id, "nama": nama, "harga": harga, "stok": stok}
    produk.append(produk_baru)
    print(f"Produk {nama} telah ditambahkan.") 

# Fungsi untuk mengedit produk (hanya admin)
def edit_produk():
    if not is_admin():
        print("Anda tidak memiliki izin untuk mengedit produk.")
        return

    tampilkan_produk()
    id_produk = int(input("Pilih ID produk yang ingin diedit: "))

    for product in produk:
        if product['id'] == id_produk:
            nama = input(f"Nama ({product['nama']}): ")
            harga = input(f"Harga ({locale.currency(product['harga'], grouping=True)}): ")
            stok = input(f"Stok ({product['stok']}): ")

            if nama:
                product['nama'] = nama
            if harga:
                product['harga'] = int(harga)
            if stok:
                product['stok'] = int(stok)

            print(f"Produk ID {id_produk} telah diperbarui.")
            return

    print("Produk tidak ditemukan.")

# Fungsi untuk menghapus produk (hanya admin)
def hapus_produk():
    if not is_admin():
        print("Anda tidak memiliki izin untuk menghapus produk.")
        return

    tampilkan_produk()
    id_produk = int(input("Pilih ID produk yang ingin dihapus: "))

    for product in produk:
        if product['id'] == id_produk:
            produk.remove(product)
            print(f"Produk ID {id_produk} telah dihapus.")
            return

    print("Produk tidak ditemukan.")

# Fungsi untuk melakukan transaksi (hanya pembeli)
def transaksi():
    if not is_pembeli():
        print("Anda tidak memiliki izin untuk melakukan transaksi.")
        return

    tampilkan_produk()
    id_produk = int(input("Pilih ID produk yang ingin dibeli: "))

    for product in produk:
        if product['id'] == id_produk:
            jumlah = int(input(f"Jumlah {product['nama']} yang ingin dibeli: "))
            if jumlah <= product['stok']:
                total_harga = jumlah * product['harga']
                product['stok'] -= jumlah
                keranjang.append({"id_produk": id_produk, "nama_produk": product['nama'], "jumlah": jumlah, "total_harga": total_harga})
                print(f"{jumlah} {product['nama']} telah ditambahkan ke keranjang belanja.")
            else:
                print(f"Stok {product['nama']} tidak mencukupi.")
            return

    print("Produk tidak ditemukan.")

# Fungsi untuk menampilkan keranjang belanja
def tampilkan_keranjang():
    if not is_pembeli():
        print("Anda tidak memiliki izin untuk melihat keranjang belanja.")
        return

    if not keranjang:
        print("Keranjang belanja Anda kosong.")
        return

    table = PrettyTable()
    table.field_names = ["ID Produk", "Nama Produk", "Jumlah", "Total Harga"]
    for item in keranjang:
        table.add_row([item["id_produk"], item["nama_produk"], item["jumlah"], locale.currency(item['total_harga'], grouping=True)])
    print(table)

# Fungsi untuk menghapus item dari keranjang(hanya pembeli)
def hapus_dari_keranjang():
    if not is_pembeli():
        print("Anda tidak memiliki izin untuk menghapus item dari keranjang.")
        return

    tampilkan_keranjang()
    id_produk = int(input("Pilih ID produk yang ingin dihapus dari keranjang: "))
    for item in keranjang:
        if item['id_produk'] == id_produk:
            keranjang.remove(item)
            print(f"Produk ID {id_produk} telah dihapus dari keranjang.")
            return

    print("Produk tidak ditemukan dalam keranjang.")

1. Menu Awal untuk Login User Admin dan Pembeli

![Cuplikan layar 2023-10-10 053534](https://github.com/DanilPrtmaa/Postest_2/assets/146010899/2f12798e-162e-4267-a519-09b5bbb56aaa)
