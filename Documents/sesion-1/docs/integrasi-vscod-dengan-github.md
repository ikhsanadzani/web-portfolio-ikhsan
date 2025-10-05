. Buka Visual Code Studio
2. lalu buka terminal di vscode
3. tekan new terminal
4. ikuti langkah berikut ini yang pasti akan muncul diterminal kalian: 
"$ ssh-keygen -t ed25519 -C "youremail.com" Generating public/private ed25519 key pair."

Enter file in which to save the key (/home/whybukos/.ssh/id_ed25519): file {nama kan file kalian}

Enter passphrase for "file" (empty for no passphrase): (langsung enter aja)

Enter same passphrase again:

5. lalu nanti kembali lagi ke awal 

6. terus kita akan membuat direktori dengan perintah:
mkdir .ssh
cd 
ls (setelah ls akan muncul isi file mirip seperti ini)

Desktop  Downloads  file.pub  Pictures  Templates  yay
Documents  file  Music  Public  Videos

lalu kita akan memindahkan file yang tadi kalian buat ke file.pub dengan perintah : 
- mv file file.pub.ssh/
- cat .ssh/file
- cat .ssh/file.pub
setelah itu akan muncul kunci SSH kalian 

7. lanjut kita akan membuak github, jangan lupa untuk menyalin kunci SSH yang tadi

8. Sudah di github, kalian ke profile dan klik opsi setting 

9. lalu klik opsi SSH and GPG Keys

10. klik new ssh key

11. beri nama sesuka kalian 

12. dan tempelkan ssh key yang sudah kalian salin sebelumnya

selesai.