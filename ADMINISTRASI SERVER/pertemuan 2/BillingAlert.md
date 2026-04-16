1. Menu Dashboard AWS kita pilih Billing Preference untuk mengaktifkan Alert
Masuk Menu Billing and Cost Manajemen
Pada Menu Cost Manajemen Scroll Ke bawah pilih Billing Preferences
Pilih Menu Alert Preferences klik Edit
isi Email ceklis Receive
Klik Update
![alt text](image.png)
![alt text](image-1.png)

2. Masuk Menu Cloudwatch, All Services Pilih CLoudWatch
![alt text](image-2.png)

3. Pilih Menu Create Alarm
Pastikan Region ada di US N Virginia
Klik Menu Create ALert
Klik Metric
Klik Menu Billing
Pilih Menu Total Estimated Charge
Pilih / Ceklis Mata Uang USD
Klik Select Metric
beri nama Alert = NIM_BillingAlert
COnditions Static->Greathertha-> 1 USD
Create new Topic = > NIM_BillingAlert -> Klik Create
Select an existing SNS topic - > NIM_BillingAlert
Klik Next
Alarm Name -> NIM_BillingAlert
Create Alarm
Buka Inbox/Spam Email dari AWS kemudian Klik Confirm
![alt text](image-3.png)
![alt text](image-4.png)