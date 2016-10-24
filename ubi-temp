from ubidots import ApiClient
import math
import os, glob, time, sys, datetime

# Create an ApiClient object

api = ApiClient(token='XXXXXXXXXXXXX')

# Get a Ubidots Variable

variable = api.get_variable('XXXXXXXXXXXXX')

#initiate the temperature sensor
os.system('modprobe w1-gpio')
os.system('modprobe w1-therm')

#set up the location of the sensor in the system
device_folder = glob.glob('/sys/bus/w1/devices/28*')
device_file = [device_folder[0] + '/w1_slave']

#function that grabs the raw temperature data from the sensor
def read_temp_raw(): 
    f_1 = open(device_file[0], 'r')
    lines_1 = f_1.readlines()
    f_1.close()
    return lines_1
 
#function that checks that the connection was good and strips out the temperature
def read_temp(): 
    lines = read_temp_raw()
    while lines[0].strip()[-3:] != 'YES':
        time.sleep(0.2)
        lines = read_temp_raw()
    equals_pos = lines[1].find('t=')
    temp = float(lines[1][equals_pos+2:])/1000
    temp_f = temp * 9.0 / 5.0 + 32
    return temp_f 

# Write the value to your variable in Ubidots
response = variable.save_value({"value": read_temp()})
print response
quit()

    

