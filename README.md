# 6-Tugas-Akhir-Kelompok-Pemodelan-Oseanografi
Repositori ini dibuat untuk memenuhi tugas akhir kelompok praktikum Pemodelan Oseanografi 2022. Terdapat 4 materi yang ada di respositori ini, yaitu Adveksi-Difusi 1D, Adveksi-Difusi 2D, Hidrodinamika 1D, dan Hidrodinamika 2D. Bahasa pemograman yang digunakan pada keempat materi tersebut adalah *Python* yang dapat dikerjakan pada *text editor Google Colaboratory dan Jupyter Notebook*. Modul yang digunakan pada repositori ini adalah *matplotlib*, *numpy*, dan *sys*.
# Proses Penjalanan 


# *Adveksi-Difusi 1D*


# *Adveksi-Difusi 2D*
**TEORI DASAR:** 

Adveksi yaitu mekanisme perpindahan massa suatu materi dari satu titik ke titik lainnya. Sedangkan Difusi yaitu mekanisme penyebaran konsentrasi akibat adanya kecepatan aliran dan perbedaan konsentrasi. Bentuk 2D terlihat dari beda waktu dan beda ruang.

![image](https://user-images.githubusercontent.com/105983387/169819206-a22c423e-a3d4-427b-b54d-c1e085592105.png)

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
  Input parameter
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

**_OUTPUT_:** 

![Kelompok 6](https://user-images.githubusercontent.com/106006093/169685569-5a22b2ce-9e7c-442e-b167-ccc6a44bdb83.png)
# Analisis:
Data parameter yang digunakan diantaranya tekanan, kecepatan angin, arah angin, dan temperatur air pada tanggal 22 Maret 2022 sampai 8 Mei 2022. Grafik diatas diperoleh dari hasil ekstrak data NDBC (National Data Buoy Center) milik NOAA yang kemudian diplot-kan dalam bentuk grafik. Lokasi pengamatan yaitu di stastion ID 41008 yang berada di lepas pantai Georgia, Amerika Serikat, tepatnya pada tenggara Savannah pada koordinat 31.400 N 80.866 W (31°24'0" N 80°51'59" W). Berdasarkan hasil diatas, terdapat 3 grafik dengan warna yang berbeda. Grafik pertama merupakan grafik tekanan, dari gambar tersebut tekanan di lokasi yang ditinjau menunjukkan nilai terendah sebesar 1002 hPa dan yang tertinggi 1038 hPa. Namun di setiap minggunya, grafik menggambarkan fluktuasi tekanan yang tidak konstan dimana tekanan cenderung naik turun dengan nilai terendah berada pada awal bulan April dan nilai tertinggi berada pada akhir bulan April. Begitupula dengan grafik kecepatan angin dan arah angin yang menggambarkan fluktuasi naik turun dengan kecepatan angin tertinggi sebesar 22 m/s dan yang terendah sebesar 0,1 m/s. Arah angin berkisar di 20° - 320°. Untuk grafik ketiga yaitu grafik temperatur yang digambarkan dengan warna biru langit menunjukkan fluktuasi yang tidak konstan dengan kisaran rata-rata berada di 21°C. Suhu tertinggi berada pada awal Mei dengan nilai 26°C dan yang terendah terjadi pada akhir Maret dengan nilai 17°C. Dari grafik yang terlihat, suhu dan tekanan memiliki bentuk grafik yang berbanding terbalik, begitupula dengan suhu dan kecepatan angin. Artinya ketika suhu bernilai rendah, maka tekanan dan kecepatan angin tinggi. Sedangkan untuk hubungan tekanan dan kecepatan angin yaitu linier, sehingga bentuk grafik nya hampir sama. Tekanan udara di permukaan bumi ditentukan oleh kerapatan massa udara. Semakin padat udara, semakin tinggi tekanannya. Kepadatan udara erat kaitannya dengan suhu, radiasi matahari, kelembaban dan gravitasi. Di daerah dengan udara tipis, tekanan permukaan rendah. Di daerah dengan udara padat, tekanan permukaan tinggi. Temperatur dan tekanan itu sendiri mempunyai hubungan terbalik, ketika temperatur rendah maka tekanannya tinggi karena densitas massa udara disana tinggi. Di sisi lain, ketika suhu tinggi, tekanan udara di atas rendah karena densitas massa rendah. Perbedaan tekanan ini kemudian menciptakan gerakan angin dan mempengaruhi kecepatan angin. Perbedaan tekanan udara pada daerah yang berbeda pada ketinggian yang sama disebabkan oleh perbedaan radiasi matahari yang diterima. Hal ini sesuai dengan pandangan Stewart (2008) bahwa angin bergerak dari tekanan tinggi ke tekanan rendah dan kecepatan angin ditentukan oleh laju perubahan tekanan, dimana tekanan udara mempengaruhi perubahan kecepatan angin. Besarnya kecepatan angin ini akan berhubungan dengan tinggi gelombang yang ditimbulkan oleh angin tersebut. Bila kecepatan angin tinggi maka gelombang di daerah tersebut juga akan semakin tinggi.



# Pengunduhan Script Pemodelan Oseanografi
1. Klik *releases* pada repositori ini.
2. Klik *script* yang ingin diunduh.
3. *Script* akan terunduh secara otomatis.


# *Kelompok 6 Pemodelan Oseanografi*
1. Abyan Maziakiko Nuhafizha/26050120140036/Oseanografi B
2. Anisa Margaretha Tumanggor/26050120140144/Oseanografi B
3. Bintang Febrian/26050120140132/Oseanografi B
4. Felia Iranda/26050120120033/Oseanografi A
5. Laviola Reycha Fitri Andhita/26050120120016/Oseanografi A
6. Maheswari Pitra Qonita/26050120120020/Oseanografi A
7. Satrio Harmin Galih Adi Yuwono/26050120140140/Oseanografi B
