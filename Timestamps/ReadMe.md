
#### Getting localized names of weekdays and timestamps in PHP and JavaScript
```PHP
echo 'Saturday: Lørdag<br>';
setlocale(LC_ALL,'da-DK');
echo setlocale(LC_ALL, 0) . '<br>';
echo utf8_encode(strftime("%A %d %B %Y", mktime(0, 0, 0, 12, 23, 1978))) . '<br>';
echo             strftime("%A %d %B %Y", mktime(0, 0, 0, 12, 23, 1978))  . '<br>';
$dt = new DateTime();echo $dt->format('Y-m-d_H:i:s.u') . '<br>';
```
You will see this:

    Saturday: Lørdag
    da-DK
    lørdag 23 december 1978
    l�rdag 23 december 1978
    2020-04-13_08:11:05.752100
where the timestamp is in the servers localtime.

To get the same timestamp in JavaScript:
```JS
document.write('<br>' + getDateStringServ(Date.now()));
function getDateStringServ(timestamp) {
  const plus0 = num => `0${num.toString()}`.slice(-2)
  const d = new Date(timestamp)
  const year = d.getFullYear()
  const monthTmp = d.getMonth() + 1
  const month = plus0(monthTmp)
  const date = plus0(d.getDate())
  const hour = plus0(d.getHours())
  const minute = plus0(d.getMinutes())
  const second = plus0(d.getSeconds())
  const rest = timestamp.toString().slice(-5)
  return `${year}-${month}-${date}_${hour}:${minute}:${second}.${rest}`
}
```
Yields this:

    2020-04-13_08:08:06.86925
This time the timestamp is in local time (from my Windows 10 PC)
