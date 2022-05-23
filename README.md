# 6-Tugas-Akhir-Kelompok-Pemodelan-Oseanografi
Repositori ini dibuat untuk memenuhi tugas akhir kelompok praktikum Pemodelan Oseanografi 2022. Terdapat 4 materi yang ada di respositori ini, yaitu Adveksi-Difusi 1D, Adveksi-Difusi 2D, Hidrodinamika 1D, dan Hidrodinamika 2D. Bahasa pemograman yang digunakan pada keempat materi tersebut adalah *Python* yang dapat dikerjakan pada *text editor Google Colaboratory dan Jupyter Notebook*. Modul yang digunakan pada repositori ini adalah *matplotlib*, *numpy*, dan *sys*.



# *Adveksi-Difusi 1D*


# *Adveksi-Difusi 2D*
# Teori Dasar:
Adveksi yaitu mekanisme perpindahan massa suatu materi dari satu titik ke titik lainnya. Sedangkan Difusi yaitu mekanisme penyebaran konsentrasi akibat adanya kecepatan aliran dan perbedaan konsentrasi. Bentuk 2D terlihat dari beda waktu dan beda ruang.
# Script 
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
penjelasan, script, dan output



# *Hidrodinamika 2D*
# Teori Dasar:

# Output:
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
