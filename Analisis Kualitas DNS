import subprocess
import re
import time

def nslookup_analyzer(domain):
    """Menjalankan nslookup dan menganalisis hasilnya."""
    try:
        start = time.time()
        result = subprocess.check_output(["nslookup", domain], stderr=subprocess.STDOUT, text=True)
        end = time.time()

        # Analisis hasil
        ips = re.findall(r"Address: ([\d\.]+)", result)
        query_time = round((end - start) * 1000, 2)  # dalam ms

        print("\n=== Hasil Analisis NSLookup ===")
        print(f"Domain         : {domain}")
        print(f"Jumlah IP Ditemukan : {len(ips)}")
        print(f"Daftar IP       : {', '.join(ips) if ips else 'Tidak ditemukan'}")
        print(f"Waktu Respon    : {query_time} ms")

        if len(ips) == 0:
            print("Status Analisis : DNS mungkin bermasalah atau tidak merespons.")
        elif query_time < 100:
            print("Kualitas DNS    : Sangat Baik")
        elif query_time < 300:
            print("Kualitas DNS    : Baik")
        else:
            print("Kualitas DNS    : Lambat")

    except subprocess.CalledProcessError as e:
        print("Gagal menjalankan nslookup:", e.output)

def main():
    print("=== Python NSLookup Analyzer ===")
    domain = input("Masukkan nama domain: ")
    nslookup_analyzer(domain)

if __name__ == "__main__":
    main()
