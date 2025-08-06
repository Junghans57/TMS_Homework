 Домашнее задание 5 — Часть 1  


---

#### 1. Добавить два дополнительных диска к ВМ
<img width="538" height="214" alt="image" src="https://github.com/user-attachments/assets/c694b982-ac82-4ac7-9755-153d7be8fdcd" />


---

#### 2. Установить на ВМ postgresql, убедиться что он запущен

<img width="1016" height="361" alt="image" src="https://github.com/user-attachments/assets/dc7ea69e-bb73-434e-b3b8-ef2521db522a" />


---

#### 3. Выяснить, в какой директории postgres хранит данные

```bash
/var/lib/pgsql/data
```

<img width="299" height="206" alt="image" src="https://github.com/user-attachments/assets/2c518ee9-b556-4c73-90c6-bfd1a237745a" />


---

#### 4. На одном новом диске создать 2 раздела (обычных, с помощью fdisk)

<img width="713" height="1027" alt="image" src="https://github.com/user-attachments/assets/cdd7ea33-2cc2-4368-a036-5600c944bf82" />


---

#### 5. Второй диск полностью отдать под LVM:

* сделать из него PV

<img width="534" height="73" alt="image" src="https://github.com/user-attachments/assets/e957b079-156a-46a8-8226-0e48f56ab8a8" />



* из PV сделать VG

<img width="554" height="109" alt="image" src="https://github.com/user-attachments/assets/f58926e2-fac9-4f32-be6d-2af63dfbe373" />


* из VG отрезать раздел под данные postgresql

<img width="762" height="72" alt="image" src="https://github.com/user-attachments/assets/7b7b2ccd-2899-43b3-a87f-0f49452f2bcd" />


---

#### 6. Смонтировать созданный раздел в директорию, которую нашли в задании 3 (не забудьте сделать бэкап директории); проверить что postgres не сломался и работает

<img width="1018" height="1244" alt="image" src="https://github.com/user-attachments/assets/662488ef-acb2-4460-ac79-fcfa48c56af3" />

<img width="1016" height="103" alt="image" src="https://github.com/user-attachments/assets/160eb956-4a69-4655-8754-9b0c5b61674a" />


---

#### 7. Создать из двух разделов на оставшемся диске два PV

<img width="590" height="164" alt="image" src="https://github.com/user-attachments/assets/6f8120db-acca-4950-859d-86d0892dbef1" />


---

#### 8. Добавить их в сущеуствующую VG

<img width="732" height="94" alt="image" src="https://github.com/user-attachments/assets/2886c26c-06a0-4437-bf7c-bcb6082b088a" />


---

#### 9. Увеличить размер LV под данными postgres

<img width="919" height="52" alt="image" src="https://github.com/user-attachments/assets/6e42dcc9-718b-4939-92f4-2b95bc248075" />
<img width="851" height="309" alt="image" src="https://github.com/user-attachments/assets/4869c421-4664-4549-b5f3-e1f3cfb47c1f" />

---

