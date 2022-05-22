# 6-Tugas-Akhir-Kelompok-Pemodelan-Oseanografi
Repositori ini dibuat untuk memenuhi tugas akhir kelompok praktikum Pemodelan Oseanografi 2022. Terdapat 4 materi yang ada di respositori ini, yaitu Adveksi-Difusi 1D, Adveksi-Difusi 2D, Hidrodinamika 1D, dan Hidrodinamika 2D. Bahasa pemograman yang digunakan pada keempat materi tersebut adalah *Python* yang dapat dikerjakan pada *text editor Google Colaboratory dan Jupyter Notebook*. Modul yang digunakan pada repositori ini adalah *matplotlib*, *numpy*, dan *sys*.



# *Adveksi-Difusi 1D*
penjelasan dan output



# *Adveksi-Difusi 2D*
penjelasan, script, dan output



# *Hidrodinamika 1D*
penjelasan, script, dan output



# *Hidrodinamika 2D*
Teori Dasar:

Script:
# Copyright (c) 2018 Siphon Contributors.
# Distributed under the terms of the BSD 3-Clause License.
# SPDX-License-Identifier: BSD-3-Clause
"""
NDBC Bouy Meteorological Data Request
=====================================
The NDBC keeps a 45-day recent rolling file for each bouy. This examples shows how to access
the basic meteorogical data from a buoy and make a simple plot.
"""

import matplotlib.pyplot as plt

from siphon.simplewebservice.ndbc import NDBC

####################################################
# Get a pandas data frame of all of the observations, meteorogical data is the default
# observation set to query
df = NDBC.realtime_observations('41008') #Station ID
df.head()

##############################################
# Let's make a simple times series plot to checkout what the data look like.
fig, (ax1, ax2, ax3) = plt.subplots(3, 1, figsize=(12, 10))
ax2b = ax2.twinx()

# Pressure
ax1.plot(df['time'], df['pressure'], color='black')
ax1.set_ylabel('Pressure [hPa]')
fig.suptitle('Kelompok 6_Oseanografi 2020', fontsize=18)


# Wind Speed, gust, direction
ax2.plot(df['time'], df['wind_speed'], color='tab:orange')
ax2.plot(df['time'], df['wind_gust'], color='tab:olive', linestyle='--')
ax2b.plot(df['time'], df['wind_direction'], color='tab:blue', linestyle='-')
ax2.set_ylabel('Wind Speed [m/s]')
ax2b.set_ylabel('Wind Direction')


# Water temperature
ax3.plot(df['time'], df['water_temperature'], color='tab:brown')
ax3.set_ylabel('Water Temperature [degC]')

plt.show()

Output:

Analisis:



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
