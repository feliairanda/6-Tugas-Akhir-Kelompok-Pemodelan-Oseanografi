# 6-Tugas-Akhir-Kelompok-Pemodelan-Oseanografi
Repositori ini dibuat untuk memenuhi tugas akhir kelompok praktikum Pemodelan Oseanografi 2022. Terdapat 4 materi yang ada di respositori ini, yaitu Adveksi-Difusi 1D, Adveksi-Difusi 2D, Hidrodinamika 1D, dan Hidrodinamika 2D. Bahasa pemograman yang digunakan pada keempat materi tersebut adalah *Python* yang dapat dikerjakan pada *text editor Google Colaboratory dan Jupyter Notebook*. Modul yang digunakan pada repositori ini adalah *matplotlib*, *numpy*, dan *sys*.

# Proses Penjalanan *Script Python*
- Masuk ke _command_ dan ketik perintah 'Jupyter Notebook'
- Pilih _New_ atau Anda bisa membuka _project_ yang sudah dikerjakan sebelumnya
- Masukan dan susun _script_ Python Anda dan klik _Run_ untuk menjalankan _script_ tersebut

# *Adveksi-Difusi 1D*
**LATAR BELAKANG**

Persamaan diferensial parsial merupakan persamaan diferensial yang melibatkan turunan parsial dari satu atau lebih variabel terikat dengan lebih dari satu variabel bebas. Persamaan diferensial dapat digunakan untuk memodelkan permasalahan sehari-hari yang biasa ditemukan seperti konduksi panas pada batang atau lempengan, menentukan muatan atau arus dalam rangkaian listrik, menentukan getaran kawat atau membran, tingkat pertumbuhan populasi, dan masih banyak lagi. Salah satu contoh permasalahan yang dapat dimodelkan dalam persamaan diferensial adalah difusi dan adveksi. Difusi merupakan proses transportasi materi dari suatu sistem ke bagian yang lain sebagai hasil dari gerakan molekul acak. Sedangkan, adveksi merupakan proses transportasi berupa aliran rata-rata atau arus, seperti sungai atau gerakan pasang surut yang digerakkan oleh gaya gravitasi atau tekanan dan berupa gerak horizontal. Persamaan difusi-adveksi merupakan model matematika yang menggambarkan proses transportasi suatu zat yang dipengaruhi gaya gravitasi dan penyebaran sekaligus. 

**PERSAMAAN**

Persamaan difusi-adveksi satu dimensi (1D) dapat ditulis sebagai berikut :

![image](https://user-images.githubusercontent.com/105999254/169869170-fdbf74a6-9cb8-4f19-b07d-030bf108c452.png)

Dengan :

V : Kecepatan Adveksi

D : Koefisien Difusi

Persamaan di atas terlebih dahulu diubah dalam bentuk operator diferensial L sampai bentuk operator adjoin L*.Setelah itu, domain semi-tak hingga dan syarat batas Dirichlet diterapkan pada solusi umum persamaan difusi-adveksi. Setelah melalui tahap-tahap tersebut, diperoleh solusi principal dan solusi reguler. Solusi principal merupakan solusi dari bentuk tak homogen persamaan diferensial tanpa memperhatikan syarat batas. Sedangkan, solusi reguler merupakan solusi dari bentuk homogen persamaan diferensial dengan syarat batas. Setelah diperoleh solusi principal dan solusi reguler, fungsi Green didapatkan dengan menjumlahkan keduanya. Terakhir, jika fungsi Green disubstitusikan ke solusi umum persamaan difusi-adveksi pada domain semi-tak hingga dan syarat batas Dirichlet, maka solusi persamaan difusi-adveksi dapat diperoleh dengan menyelesaikan integrasinya.

# *Adveksi-Difusi 2D*
**TEORI DASAR:** 

Adveksi yaitu mekanisme perpindahan massa suatu materi dari satu titik ke titik lainnya. Sedangkan Difusi yaitu mekanisme penyebaran konsentrasi akibat adanya kecepatan aliran dan perbedaan konsentrasi. Bentuk 2D terlihat dari beda waktu dan beda ruang.

![image](https://user-images.githubusercontent.com/105983387/169831359-81180288-ad89-4b57-b053-f9cb0f05f55e.png)

- Persamaan adveksi difusi merupakan persamaan umum yang menggambarkan proses adveksi serta difusi dimana menggambarkan sebuah perpindahan dan perluasan atau penyebaran sebuah konsentrasi zat yang dipengaruhi oleh gaya - gaya tertentu dalam arah horizontal. Dimana persamaan Adveksi dan Difusi 2 Dimensi yang terjadi akan diolah untuk membentuk suatu persamaan model 2 Diumensi yang mendekati proses kejadian di alam. 
- Sebelum memulai pemrograman Adveksi-Difusi 2 Dimensi, dibutuhkan beberapa library dimana adanya library membuat pemrograman python menjadi lebih sederhana dan nyaman bagi programmer karena tidak perlu menulis kode yang sama berulang kali untuk program yang berbeda, yaitu numpy, sys dan matplotlib. Library Numpy akan bekerja untuk menyimpan data sebagai grid atau matriks. Sys berfungsi untuk mengakses konfigurasi interpreter pada saat runtime dan berinteraksi dengan environment sistem operasi. Library Matplotlib akan berfungsi untuk menggambarkan hasil running ke dalam plot grafik. 
- Dalam pemodelan kali ini juga menggunakan beberapa parameter terkait yaitu : C = kecepatan aliran, Q = kriteria kestabilan, Dt = perubahan waktu, Dx = jarak antar grid horizontal, Dy = jarak antar grid vertical, Px = jumlah polutan pada sumbu x, Py = jumlah polutan pada sumbu y, dan Ic = jumlah polutan total.

**_SCRIPT_**

Import library yang dibutuhkan dan pendefinisian
```
import matplotlib.pyplot as plt
import numpy as np
import sys
#%%
def percentage(part, whole):
        percentage = 100 * float(part)/float(whole)
        return str(round(percentage,2)) + "%"
```
 _Input_ parameter
 ```
 #input parameter awal
C = 1.33 #Arus/Konstanta Adveksi
ad = 1.33 #Konstanta Difusi
theta = 0 + 33 #Arah Arus (Geographics Convertion (0 degree N))
#parameter lanjutan
q = 0.95 #syarat kestabilan
x = 500 #Jumlah Grid x
y = 500 #Jumlah Grid y
dx = 5
dy = 5
Tend = 100 + 3 #Waktu Simulasi
dt = 0.5
#Polutan
px = 250 #Grid x polutan dibuang
py = 230 + 3 #Grid x polutan dibuang
Ka = 1000 + 33 #Jumlah Polutan (Ic)
```
  Perhitungan U dan V
 ```
 u = C * np.sin(theta*np.pi/180)
v = C * np.cos(theta*np.pi/180)
dt_count = 1/((abs(u)/(q*dx))+(abs(v)/(q*dy))+(2*ad/(q*dx**2))+(2*ad/(q*dx**2)))
```
  Perhitungan titik lepas Polutan
 ```
 px1 = int (px/dx)
py1 = int (py/dy)
```
  Penyederhanaan fungsi dan perhitungan CFL
 ```
 lx = u*dt/dx
ly = v*dt/dy
ax = ad*dt/dx**2
ay = ad*dt/dy**2
cfl = (2*ax + 2*ay + abs(lx) + abs(ly))
 if cfl >= q:
    print('CFL Violated, Please use dt :'+str(round(dt_count,4)))
    sys.exit()
 ```
  Pembuatan Grid
  ```
  x_grid = np.linspace(0-dx, x+dx, Nx+2) #Untuk GhostNode pada Ujung Boundary
y_grid = np.linspace(0-dy, y+dx, Ny+2) #Untuk GhostNode pada Ujung Boundary
t = np.linspace(0, Tend, Nt+1)
x_mesh,y_mesh = np.meshgrid(x_grid, y_grid)
F = np.zeros((Nt+1,Ny+2,Nx+2))
```
  Iterasi
  ```
  for n in range (0,Nt):
    for i in range (1,Ny+1):
        for j in range (1,Nx+1):
            F[n+1,i,j]=((F[n,i,j]*(1-abs(lx)-abs(ly))) + (0.5*(F[n,i-1,j]*(ly+abs(ly)))) + (0.5*(F[n,i+1,j]*(abs(ly)-ly))))
    #Kondisi Batas (Dirichlet Condition)
    F[n+1,0,:] = 0 #Batas Bawah
    F[n+1,:,0] = 0 #Batas Kiri
    F[n+1,Ny+1,:] = 0 #Batas Atas
    F[n+1,:,Nx+1] = 0 #Batas Kanan
  ```    
  Perintah untuk print hasil metode adveksi-difusi 2D
  ```
  #Output Gambar
    plt.clf()
    plt.pcolor(x_mesh, y_mesh, F[n+1,:,:],cmap = 'jet',shading = 'auto', edgecolors = 'k')
    cbar = plt.colorbar(orientation = 'vertical',shrink = 0.95, extend ='both')
    cbar.set_label(label='concentration', size = 8)
    #plt.clim(0,100)
    plt.title('Kelompok 6_Oseanografi 2020 - Skenario 1 \n t='+str(round(dt*(n+1),3))+', Kondisi Awal='+str(Ka),fontsize=10)
    plt.xlabel('x_grid',fontsize=9)
    plt.ylabel('y_grid',fontsize=9)
    plt.axis([0,x,0,y])
    #plt.pause(0.01)
    plt.savefig(str(n+1)+'.png', dpi = 300)
    plt.close()
    print('running timestep ke :' + str(n+1) + ' dari :' + str(Nt) + ' ('+ percentage(n+1,Nt)+')')
  ```
 **OUTPUT**
 
   Pada t=0.5   ![1](https://user-images.githubusercontent.com/106000656/170006015-39422510-1a7c-4fd3-9a8c-a2dfaa0b2554.png)
   Pada t=103   ![206](https://user-images.githubusercontent.com/106000656/170006240-ee9ab714-4305-4a11-ae5d-d00c9e7869c1.png)
 PEMBAHASAN :
- Adapun nilai CFL atau Courant-Friedrichs-Lewy adalah kondisi yang diperlukan untuk konvergensi sambil menyelesaikan persamaan diferensial parsial tertentu secara numeric, dimana nilai CFL erat kaitanya dengan hasil pemodelan. Nilai CFL biasanya memiliki rentangan 0 – 1 dimana jika melebihi akan membuat hasil pemodelan tidak valid atau eror.
- Adapun hubungan antara nilai C dan Ad dimana dijelaskan nilai C merupakan sebuah besaran kecepatan polutan dan nilai Ad merupakan sebuah koefisien difusi. Jika nilai C=0 dan nilai ad=1, maka dapat dipastikan bahwa polutan tidak akan bergerak dan tetap di tempat yang sama tetapi mengalami perubahan dan penyebaran (difusi) hal ini dikarenakan kecepatan polutan tidak ada dan dipastikan akan tepat pada satu titik atau grid. 
- Hasil tersebut perlu disempurnakan, mengingat ini adalah pemodelan 2 dimensi dimana hanya mengikat dua ruang saja yaitu x dan y. Pelengkapan data - data terkait kondisi perairan dan konsentrasi polutan seperti pasang surut, musim, fluktuasi konsentrasi dan debit diperlukan sehingga akan lebih representatif. Kemudian untuk mendapatkan validasi yang lebih baik lagi dibutuhkan juga pengukuran data arus dilapangan ( Handiani et al., 2008).

# *Hidrodinamika 1D*
**TEORI DASAR:**  
Hidrodinamika merupakan salah satu cabang ilmu pengetahuan yang mempelajari gerak liquid atau gerak fluida cair khususnya gerak air yang dipengaruhi oleh gaya eksternal dan internal. Terdapat dua jenis transport dalam hidrodinamika, yaitu Adveksi dan Difusi. Pada pemodelan hidrodinamika 1D, digunakan konversi massa dan hukum momentum yang diperuntukkan untuk simulasi tinggi muka air laut dan aliran arus yang dibangkitkan oleh angin, gelombang, pasang surut, dll

**PERSAMAAN UTAMA**

![image](https://user-images.githubusercontent.com/105919702/169822268-60a1846d-10e2-4afe-a75a-9f69b561798f.png)
![image (1)](https://user-images.githubusercontent.com/105919702/169822291-9e68c034-dedd-462a-a055-3e17f3cb56dc.png)


**PERSAMAAN PEMBANGUN**

![image (2)](https://user-images.githubusercontent.com/105919702/169822321-3cc43449-d80c-462a-a06a-0b00e1bd4dc3.png)
![image (3)](https://user-images.githubusercontent.com/105919702/169822336-653ad4db-7bc5-4370-838f-919bf20676b4.png)


**PERSAMAAN TRANSPORT**

![image (4)](https://user-images.githubusercontent.com/105919702/169822859-a7364600-eea6-4948-bcd9-46d61ca18e68.png)
![image (5)](https://user-images.githubusercontent.com/105919702/169822888-40c993f1-0fe3-4035-a772-a3101844906a.png)


**DISKRETISASI**

![image (6)](https://user-images.githubusercontent.com/105919702/169823081-a6a70b29-524c-44d6-85f3-f466d3bf1500.png)
![image (7)](https://user-images.githubusercontent.com/105919702/169823117-b3c32d30-96e7-4da2-9436-afb0c0fcb239.png)


**PENYELESAIAN ANALITIK**

![image (8)](https://user-images.githubusercontent.com/105919702/169823289-99cab16c-43b4-4b07-93a2-f7eab5f60999.png)
![image (9)](https://user-images.githubusercontent.com/105919702/169823318-a0d84b7d-f3b7-4319-901d-db6853641161.png)


**_SCRIPT_**

Import Modul
```
import matplotlib.pyplot as plt
import numpy as np
```

Proses Awal
```
p = 5000 #Panjang Grid
T = 1200 #Waktu Simulasi
A = 0.5 #Amplitudo
D = 15 #Depth
dt = 2
dx = 100
To = 300 #Periode

g = 9.8
pi = np.pi
C = np.sqrt(g*D) #Kecepatan arus
s = 2*pi/To #Kecepatan sudut gelombang
L = C*To #Panjang gelombang
k = 2*pi/L #Koefisien panjang gelombang
Mmax = int(p//dx)
Nmax = int(T//dt)

zo = [None for _ in range(Mmax)]
uo = [None for _ in range(Mmax)]

hasilu = [None for _ in range(Nmax)]
hasilz = [None for _ in range(Nmax)]

for i in range(1, Mmax+1):
  zo[i-1] = A*np.cos(k*(i)*dx)
  uo[i-1] = A*C*np.cos(k*((i)*dx+(0.5)*dx))/(D+zo[i-1])
for i in range(1, Nmax+1):
  zb = [None for _ in range(Mmax)]
  ub = [None for _ in range(Mmax)]
  zb[0] = A*np.cos(s*(i)*dt)
  ub[-1] = A*C*np.cos(k*L-s*(i)*dt)/(D+zo[-1])
  for j in range(1, Mmax):
    ub[j-1] = uo[j-1]-g*(dt/dx)*(zo[j]-zo[j-1])
  for k in range(2, Mmax+1):
    zb[k-1] = zo[k-1]-(D+zo[k-1])*(dt/dx)*(ub[k-1]-ub[k-2])
    hasilu[i-1] = ub
    hasilz[i-1] = zb
  for p in range(0, Mmax):
    uo[p] = ub[p]
    zo[p] = zb[p]
```

Pembuatan Grafik
```
def rand_col_hex_string():
    return f'#{format(np.random.randint(0,16777215), "#08x")[2:]}'
    
hasilu_np = np.array(hasilu)
hasilz_np = np.array(hasilz)

fig0, ax0 = plt.subplots(figsize=(12,8))
for i in range(1, 16):
    col0 = rand_col_hex_string()
    line, = ax0.plot(hasilu_np[:,i-1], c=col0, label=f'n={i}')
    ax0.legend()
    
    ax0.set(xlabel='Waktu', ylabel='Kecepatan Arus', 
            title= ''' Kelompok 6_Oseanografi 2020
            Perubahan Kecepatan Arus Dalam Grid Tertentu di Sepanjang Waktu''')
    ax0.grid()
    
fig1, ax1 = plt.subplots(figsize=(12,8))
for i in range(1, 16):
    col1 = rand_col_hex_string()
    line, = ax1.plot(hasilz_np[:,i-1], c=col1, label=f'n={i}')
    ax1.legend()
    
    ax1.set(xlabel='Waktu', ylabel='Elevasi Muka Air', 
            title= ''' Kelompok 6_Oseanografi 2020
            Perubahan Elevasi Permukaan Air Dalam Grid Tertentu di Sepanjang Waktu''')
    ax1.grid()
    
fig2, ax2 = plt.subplots(figsize=(12,8))
for i in range(1, 16):
    col2 = rand_col_hex_string()
    line, = ax2.plot(hasilu_np[i-1], c=col2, label=f't={i}')
    ax2.legend()
    
    ax2.set(xlabel='Grid', ylabel='Kecepatan Arus', 
            title= ''' Kelompok 6_Oseanografi 2020
            Perubahan Kecepatan Arus Dalam Waktu Tertentu di Sepanjang Grid''')
    ax2.grid()

fig3, ax3 = plt.subplots(figsize=(12,8))
for i in range(1, 16):
    col3 = rand_col_hex_string()
    line, = ax3.plot(hasilz_np[i-1], c=col3, label=f't={i}')
    ax3.legend()
    
    ax3.set(xlabel='Grid', ylabel='Elevasi Muka Air', 
            title= ''' Kelompok 6_Oseanografi 2020
            Perubahan Elevasi Permukaan Air Dalam Waktu Tertentu di Sepanjang Grid''')
    ax3.grid()
    
plt.show()
```

**OUTPUT**

![Perubahan Elevasi Permukaan Air Dalam Grid Tertentu di Sepanjang Waktu](https://user-images.githubusercontent.com/105919702/169825151-918a97ce-02c4-4658-9d59-3fc021b13118.png)
![Perubahan Kecepatan Arus Dalam Grid Tertentu di Sepanjang Waktu](https://user-images.githubusercontent.com/105919702/169825214-6c79d76c-4c89-4620-80db-da6fca36f5b6.png)
![Perubahan Elevasi Permukaan Air Dalam Waktu Tertentu di Sepanjang Grid](https://user-images.githubusercontent.com/105919702/169825245-c32c5a57-9461-4895-9989-de6bdd92bb3d.png)
![Perubahan Kecepatan Arus Dalam Waktu Tertentu di Sepanjang Grid](https://user-images.githubusercontent.com/105919702/169825282-0fced3b7-f3a6-4274-a125-849f44c03ded.png)







# *Hidrodinamika 2D*
**TEORI DASAR:**
 Hidrodinamika merupakan ilmu yang mempelajari tentang gerak cair dan merupakan ilmu dasar dalam hidrolika dan oseanografi. Konsep dasar hidrodinamika teoritis didasarkan pada konsepan massa dasar atau partikel fluida. Partikel partikel ini dapat dianggap sebagai corpus (kumpulan) atau alienum (benda asing dalam mekanika kontinum). 
 
 ![Screenshot (20)](https://user-images.githubusercontent.com/106001831/169841331-ca93cc18-57de-49a2-9ebc-529f7915ddcb.png)
 
Pada gambar dapat lihat konsep dasar dari hidrodinamika 1 dan 2 dimensi. Konsep dasar dari hidrodinamika 1 dimensi lebih mengkaji dengan menggunakan satu variabel saja. Dimana pada konsepan hidrodinamika 1 dimensi dijelaskan sebuah penampang diambil tegak lurus terhadap aliran sungai. Dengan waterlevel yang seragam diseluruh penampang dan tidak dipengaruhi oleh kedalaman, serta kecepatan yang seragam melintasi penampang. Sedangkan untuk konsep dasar hidrodinamika 2 dimensi lebih mengkaji dengan menggunakan dua variabel. Dimana pada konsepan hidrodinamika 2 dimensi ini dijelaskan sebagai daerah yang direpresentasikan sebagai permukaan yang kontinue. Dengan kedalaman air yang tidak pernah sama serta kecepatan air dan gelombang yang tidak pernah sama. Contoh kasus model yang dapat dikaji dengan menggunakan model 2 dimensi adalah :
1. Pemodelan Tumpahan Minyak terhadap Topografi Dasar Laut. Dimana untuk variabel 1 adalah Tumpahan Minyak dan variabel 2 adalah Ketinggian Topografi Laut.
2. Pemodelan Coastal Dynamics dan Sedimentasi Pantai. Dimana untuk variabel 1 adalah Dinamika Pesisir dan variabel 2 adalah Pergerakan Sedimen.

**PERSAMAAN**

![Screenshot (22)](https://user-images.githubusercontent.com/106001831/169990849-8a82a226-fb1e-49e9-a9f1-81f0cffb182d.png)

**_OUTPUT_:** 

![Kelompok 6](https://user-images.githubusercontent.com/106006093/169685569-5a22b2ce-9e7c-442e-b167-ccc6a44bdb83.png)




# Pengunduhan Script Pemodelan Oseanografi
1. Klik *releases* pada repositori ini.
2. Klik *script* yang ingin diunduh.
3. *Script* akan terunduh secara otomatis.


# Kelompok 6 Pemodelan Oseanografi
1. Abyan Maziakiko Nuhafizha/26050120140036/Oseanografi B
2. Anisa Margaretha Tumanggor/26050120140144/Oseanografi B
3. Bintang Febrian/26050120140132/Oseanografi B
4. Felia Iranda/26050120120033/Oseanografi A
5. Laviola Reycha Fitri Andhita/26050120120016/Oseanografi A
6. Maheswari Pitra Qonita/26050120120020/Oseanografi A
7. Satrio Harmin Galih Adi Yuwono/26050120140140/Oseanografi B


