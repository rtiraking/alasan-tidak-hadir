<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Sistem Informasi Absensi Karyawan | PT Ridho Teknologi Indonesia Raking</title>

<style>
:root{
    --red:#b11226;
    --navy:#0b1c2d;
    --white:#ffffff;
    --gray:#f4f6f8;
}

body{
    margin:0;
    font-family:"Segoe UI", Arial, sans-serif;
    background:var(--gray);
}

/* HEADER */
header{
    background:var(--navy);
    color:var(--white);
    padding:25px;
    text-align:center;
}

header h1{
    margin:0;
    font-size:26px;
}

header p{
    margin-top:5px;
    font-size:14px;
    opacity:0.9;
}

/* CONTAINER */
.container{
    max-width:1000px;
    margin:auto;
    padding:30px;
}

/* CARD */
.card{
    background:var(--white);
    padding:25px;
    border-radius:8px;
    border-top:5px solid var(--red);
    box-shadow:0 4px 10px rgba(0,0,0,.08);
    margin-bottom:30px;
}

.card h2{
    color:var(--navy);
    margin-top:0;
}

/* FORM */
label{
    font-weight:600;
    display:block;
    margin-top:15px;
}

input, select{
    width:100%;
    padding:10px;
    margin-top:6px;
    border-radius:4px;
    border:1px solid #ccc;
    font-size:14px;
}

input:focus, select:focus{
    outline:none;
    border-color:var(--navy);
}

/* BUTTON */
button{
    margin-top:20px;
    width:100%;
    padding:12px;
    background:var(--red);
    color:var(--white);
    border:none;
    border-radius:4px;
    font-size:15px;
    font-weight:600;
    cursor:pointer;
}

button:hover{
    background:#8e0e1d;
}

/* TABLE */
table{
    width:100%;
    border-collapse:collapse;
    margin-top:15px;
}

th, td{
    padding:10px;
    border:1px solid #ddd;
    text-align:center;
    font-size:14px;
}

th{
    background:var(--navy);
    color:var(--white);
}

/* FOOTER */
footer{
    background:var(--navy);
    color:var(--white);
    text-align:center;
    padding:12px;
    font-size:13px;
}
</style>
</head>

<body>

<header>
    <h1>PT Ridho Teknologi Indonesia Raking</h1>
    <p>Informasi Karyawan Tidak Masuk Kerja</p>
</header>

<div class="container">

    <!-- FORM ABSENSI -->
    <div class="card">
        <h2>Form Absensi Karyawan</h2>

        <label>Nama Karyawan</label>
        <input type="text" id="nama" placeholder="Masukkan nama lengkap">

        <label>Jabatan</label>
        <input type="text" id="jabatan" placeholder="Masukkan jabatan">

         <label>Alasan Tidak Hadir</label>
        <input type="text" id="jabatan" placeholder="Masukkan alasan">

        <label>Kategori</label>
        <select id="status">
            <option value="Izin">Izin</option>
            <option value="Sakit">Sakit</option>
            <option value="Cuti">Cuti</option>
            <option value="Terlambat">Terlambat</option>
        </select>

        <button onclick="simpanAbsensi()">Simpan Absensi</button>
    </div>

    <!-- DATA ABSENSI -->
    <div class="card">
        <h2>Data Absensi Karyawan</h2>

        <table>
            <thead>
                <tr>
                    <th>No</th>
                    <th>Nama</th>
                    <th>Jabatan</th>
                    <th>Status</th>
                    <th>Tanggal</th>
                    <th>Jam</th>
                </tr>
            </thead>
            <tbody id="tabelAbsensi"></tbody>
        </table>
    </div>

</div>

<footer>
    © 2026 PT Ridho Teknologi Indonesia | Sistem Absensi
</footer>

<script>
let dataAbsensi = JSON.parse(localStorage.getItem("absensi")) || [];

function simpanAbsensi(){
    const nama = document.getElementById("nama").value;
    const jabatan = document.getElementById("jabatan").value;
    const status = document.getElementById("status").value;

    if(nama === "" || jabatan === ""){
        alert("Nama dan jabatan wajib diisi!");
        return;
    }

    const waktu = new Date();
    const tanggal = waktu.toLocaleDateString("id-ID");
    const jam = waktu.toLocaleTimeString("id-ID");

    dataAbsensi.push({
        nama,
        jabatan,
        status,
        tanggal,
        jam
    });

    localStorage.setItem("absensi", JSON.stringify(dataAbsensi));
    tampilkanAbsensi();

    document.getElementById("nama").value="";
    document.getElementById("jabatan").value="";
}

function tampilkanAbsensi(){
    const tbody = document.getElementById("tabelAbsensi");
    tbody.innerHTML="";

    dataAbsensi.forEach((d,i)=>{
        tbody.innerHTML += `
        <tr>
            <td>${i+1}</td>
            <td>${d.nama}</td>
            <td>${d.jabatan}</td>
            <td>${d.status}</td>
            <td>${d.tanggal}</td>
            <td>${d.jam}</td>
        </tr>`;
    });
}

tampilkanAbsensi();
</script>

</body>
</html>
