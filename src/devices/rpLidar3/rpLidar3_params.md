 * | GENERAL        | serial_port     | string  | -              |   -           | Yes          | Name of the serial port                                           |       |
 * | GENERAL        | serial_baudrate | int     | -              |   -           | Yes          | Baud rate of the serial port                                       |       |
 * | GENERAL        | sample_buffer_life | int  | -              |   -           | Yes          | Keeps data in memory for some iterations, in order to complete the scan with the missing values (the scan is not always complete)       |  |
 * | GENERAL        | thread_period   | int     | ms             |   0           | No           | Acquisition thread period. The default value = 0 means maximum speed (measured duration ~75ms). It is useful to change it only if you need to slow down the device (e.g. 100ms)    |  |
 * | RPLIDAR        | motor_pwm       | int     | -              |   0           | No           | Used by internal RPLidar APIs                                     |       |
 * | RPLIDAR        | express_mode    | bool    |                | false         | No           | Check sensor datasheet  |  |
 * | RPLIDAR        | force_scan      | bool    |                | false         | No           | Check sensor datasheet  |  |
 * | RPLIDAR        | scan_mode       | string  |                | Boost         | No           | Check sensor datasheet  |  |
