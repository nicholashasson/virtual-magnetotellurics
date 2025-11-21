# Virtual-magnetotellurics
## Magnetotellurics (MT) from unshielded broadband seismometers at high-latitudes "Virtual-MT" (VMT)
## ***Welcome! Below is how to translate unshieled Alaska seismometers from the USArray/IRIS & University of Alaska databases***
### useful for determining the coherence between geomagnetic stations, which these stations behave as not physically different from magnetotelluric sensors
### sesimic sensors virtually share the geomagnetic field when beneath the auroral oval, where there is 1 million ampere current (I= 1 MA) in the ionosphere-earth waveguide. 
---------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------001
## please contact for questions [nhasson@alaska.edu] 
## access is complimenatary by Nicholas Hasson, PhD Graduate Student in Geosciences, University of Alaska Fairbanks

## Installation requirements see README.md 
## set anaconda Prompt (anaconda3) environment as "MT_ENV", see README.md for requirements (MT_ENV) C:Launch "Jupyter Notebook

import obspy
print("ObsPy version:", obspy.__version__)
#comment: returns "ObsPy version: 1.4.2"

st_bhz = client.get_waveforms ("AK", "POKR", "*", "BHZ", t1, t2)
print(st_bhz)
2 Trace(s) in Stream:

#example_return: 
# AK.POKR.01.BHZ | 2024-05-11T00:00:00.000000Z - 2024-05-11T09:37:46.180000Z | 50.0 Hz, 1733310 samples
# AK.POKR..BHZ   | 2024-05-11T00:00:00.000000Z - 2024-05-11T09:37:46.180000Z | 50.0 Hz, 1733310 samples

from obspy.clients.fdsn import Client
from obspy import UTCDateTime

client = Client("IRIS")

t1 = UTCDateTime("2022-03-01T00:00:00")
t2 = UTCDateTime("2022-03-02T00:00:00")

# Option 1: blank location code
st_bhz = client.get_waveforms("AK", "POKR", "", "BHZ", t1, t2)

# Option 2: explicit 01
# st_bhz = client.get_waveforms("AK", "POKR", "01", "BHZ", t1, t2)

print(st_bhz)
st_bhz.plot()


<img width="852" height="579" alt="image" src="https://github.com/user-attachments/assets/58bcedcb-e6c7-449a-bb9e-9115e10a3078" />

tr = st_bhz[0].copy()
tr.detrend("linear")
tr.detrend("demean")

tr_2_20mHz = tr.copy().filter(
    "bandpass",
    freqmin=0.002,  # 2 mHz
    freqmax=0.02,   # 20 mHz
    corners=4,
    zerophase=True
)

tr_2_20mHz.plot()

<img width="870" height="537" alt="image" src="https://github.com/user-attachments/assets/b8841a49-ed97-45a7-9798-a6b188115a46" />

st_lhz = client.get_waveforms("AK", "POKR", "", "LHZ", t1, t2)
tr_lhz = st_lhz[0].copy().detrend("linear").detrend("demean")

tr_lhz_filt = tr_lhz.copy().filter(
    "bandpass",
    freqmin=0.002, freqmax=0.02,
    corners=4, zerophase=True
)

tr_lhz_filt.plot()

<img width="859" height="535" alt="image" src="https://github.com/user-attachments/assets/92cc87f9-265f-4205-ac68-405da4e9f9ee" />

from obspy.clients.fdsn import Client
from obspy import UTCDateTime

client = Client("IRIS")

t1 = UTCDateTime("2024-05-11T0:00:00")
t2 = UTCDateTime("2024-05-11T10:30:00")

# Option 1: blank location code
st_bhz = client.get_waveforms("AK", "POKR", "", "BHZ", t1, t2)

# Option 2: explicit 01
# st_bhz = client.get_waveforms("AK", "POKR", "01", "BHZ", t1, t2)

print(st_bhz)
st_bhz.plot()

<img width="860" height="582" alt="image" src="https://github.com/user-attachments/assets/7201e250-333a-4507-9348-957ab75b2777" />


tr = st_bhz[0].copy()
tr.detrend("linear")
tr.detrend("demean")

tr_2_20mHz = tr.copy().filter(
    "bandpass",
    freqmin=0.002,  # 2 mHz
    freqmax=0.02,   # 20 mHz
    corners=4,
    zerophase=True
)

tr_2_20mHz.plot()

<img width="847" height="541" alt="image" src="https://github.com/user-attachments/assets/7c61b47b-8f36-44f5-b462-0250eb804fe6" />

st_lhz = client.get_waveforms("AK", "POKR", "", "LHZ", t1, t2)
tr_lhz = st_lhz[0].copy().detrend("linear").detrend("demean")

tr_lhz_filt = tr_lhz.copy().filter(
    "bandpass",
    freqmin=0.002, freqmax=0.02,
    corners=4, zerophase=True
)

tr_lhz_filt.plot()




