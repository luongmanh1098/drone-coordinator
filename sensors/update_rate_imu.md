Based on [issue](https://github.com/mavlink/mavros/issues/1346)

# Adjust imu rate through application

Download [QGroundControl](https://docs.qgroundcontrol.com/master/en/getting_started/download_and_install.html)
```
sudo usermod -a -G dialout $USER
sudo apt-get remove modemmanager -y
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
```
```
chmod +x ./QGroundControl.AppImage
```
Restart or logout your PC.
```
sudo chmod 666 /dev/ttyACM0 #px4 serial device
./QGroundControl.AppImage  (or double click)
```
Be sure your px4 is connect to PC.

On QGroundControl window, Click Analyze (A sheet with magnifying glass symbol on menu bar) >> MAVLink Console

On MAVLink Console:
```
cd /fs/microsd/etc
echo "mavlink stream -d /dev/ttyACM0 -s HIGHRES_IMU -r 100" > extras.txt
```
Note: 
If you want to update exist extras.txt file, you can do:
```
cd /fs/microsd/etc
rm extras.txt
echo "mavlink stream -d /dev/ttyACM0 -s HIGHRES_IMU -r 100" > extras.txt
```
Note:
On PX4, its only effects topic: /mavros/imu/data_raw. If you want to update rate on topic /mavros/imu/data too, you need to add all these line (recommend):
```
mavlink stream -d / dev / ttyACM0 -s ATTITUDE -r 100
mavlink stream -d / dev / ttyACM0 -s ATTITUDE_QUATERNION -r 100
mavlink stream -d / dev / ttyACM0 -s HIGHRES_IMU -r 100
```
# Adjust imu rate through sd card

You can easily config extras.txt through sd card. Just remove sd card from px4 and insert into your laptop. After, you can modify extras.txt file.
