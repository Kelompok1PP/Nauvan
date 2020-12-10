# Project
    from paramiko.client import SSHClient, AutoAddPolicy
    import sys
    import socket
    # from getpass import getpass
    ssh = '192.168.100.155'
    password = 'Lovaaa22'
    username = 'Raditya'

    ssh2 = '192.168.100.153'
    password2 = 'Lovaaa22'
    username2 = 'Raditya'


    client = []
    status = []
    client.append(SSHClient())
    client.append(SSHClient())


    client[0].set_missing_host_key_policy(AutoAddPolicy())
    try:
      client[0].connect(ssh, 22, username, password, timeout=5)
      status.append('CLIENT SEDANG ONLINE')
    except (socket.gaierror, socket.timeout):
        status.append('CLIENT SEDANG OFFLINE')

    client[1].set_missing_host_key_policy(AutoAddPolicy())
    try:
       client[1].connect(ssh2, 22, username2, password2, timeout=5)
       status.append('CLIENT SEDANG ONLINE')
    except (socket.gaierror, socket.timeout):
       status.append('CLIENT SEDANG OFFLINE')





    def pemilihan(a):
        file1 = open("file_send.txt", "w")
        joined = ','.join(map(str, a))
        file1.write(joined)
        file1.close()


    def prosesprogram(b):
        print("________________________________________________________\n")
        try:
            sftp = b.open_sftp()
            sftp.put('./file_send.txt', './input.txt')
            stdin, stdout, stderr = b.exec_command('python3 final.py')
            baris = stdout.readlines()
            baris_err = stderr.readlines()

            for i in baris_err:
                print(i)
            for i in baris:
                print(i)
        except:
           print("Client ini sedang OFFLINE")

    bangun_datar = True
    while(bangun_datar):
        a = ['0', '0' , '0' , '0' , '0' , '0' , '0' , '0' , '0']
        print("________________________________________________________\n")
        print("Menghitung Luas Segitiga : ")
        a[0] = input("Masukkan Alas     =\t")
        a[1] = input("Masukkan Tinggi   =\t")
        print("\n")
        print("Menghitung Keliling Segitiga : ")
        a[2] = input("Masukkan sisi a   =\t")
        a[3] = input("Masukkan sisi b   =\t")
        a[4] = input("Masukkan sisi c   =\t")
        print("\n")
        print("Menghitung Luas Persegi : ")
        a[5] = input("Masukkan sisi     =\t")
        print("\n")
        print("Menghitung Keliling Persegi : ")
        a[6] = input("Masukkan sisi     =\t")
        print("\n")
        print("Menghitung Luas Lingkaran : ")
        a[7] = input("Masukkan jari-jari lingkaran  =\t")
        print("\n")
        print("Menghitung Keliling Lingkaran : ")
        a[8] = input("Masukkan jari-jari lingkaran =\t")

        print("\n")
        print('''Client                                                           
        1. {}. Status : {} 
        2. {}. Status : {}                                 
        3. Pakai Semua Client ONLINE?
                               
        '''.format(ssh,  status[0],
                   ssh2,  status[1])
              )

        input_menu = input('Pilih Client yang ingin digunakan : ')
        if (input_menu == '1'):
            pemilihan(a)
            prosesprogram(client[0])
        elif (input_menu == '2'):
            pemilihan(a)
            prosesprogram(client[1])
        elif (input_menu == '3'):
            pemilihan(a)
            prosesprogram(client[0])
            prosesprogram(client[1])

        selesai = input("Apakah Ingin Mengakhiri Program?(y/n)")
        if (selesai == 'y'):
           for i in client:
               i.close()
           sys.exit()
