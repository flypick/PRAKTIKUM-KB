import random
import datetime
from task_operations import add_task, view_tasks, remove_task

def main():
    while True:
        print("\nMenu:")
        print("1. Tambah Tugas")
        print("2. Lihat Tugas")
        print("3. Hapus Tugas")
        print("4. Keluar")
        choice = input("Pilih opsi (1/2/3/4): ")

        if choice == "1":
            task_name = input("Masukkan nama tugas: ")
            add_task(task_name)
        elif choice == "2":
            view_tasks()
        elif choice == "3":
            try:
                task_id = int(input("Masukkan ID tugas yang akan dihapus: "))
                remove_task(task_id)
            except ValueError:
                print("ID harus berupa angka.")
        elif choice == "4":
            print("Keluar dari program.")
            break
        else:
            print("Pilihan tidak valid. Silakan coba lagi.")

if __name__ == "__main__":
    main()

# task_operations.py

tasks = [] 

def add_task(task_name):
    task = {
        "id": random.randint(1000, 9999), 
        "name": task_name,
        "timestamp": datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") 
    }
    tasks.append(task)
    print(f"Tugas '{task_name}' telah ditambahkan dengan ID {task['id']}.")

def view_tasks():
    if not tasks:
        print("Belum ada tugas yang ditambahkan.")
    else:
        print("\nDaftar Tugas:")
        for task in tasks:
            print(f"ID: {task['id']} | Nama: {task['name']} | Waktu: {task['timestamp']}")

def remove_task(task_id):
    global tasks
    for task in tasks:
        if task["id"] == task_id:
            tasks.remove(task)
            print(f"Tugas dengan ID {task_id} telah dihapus.")
            return
    print("Tugas tidak ditemukan.")
