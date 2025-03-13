import socket
import threading

# Function to scan a specific port
def scan_port(ip, port):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)
        result = sock.connect_ex((ip, port))
        if result == 0:
            print(f"[+] Open port: {port}")
        sock.close()
    except Exception as e:
        print(f"[-] Error with port {port}: {e}")

# Main entry point of the script
def main():
    target = input("Enter the IP or domain to scan: ")
    start_port = int(input("Start port: "))
    end_port = int(input("End port: "))

    print(f"\nScanning {target} from port {start_port} to {end_port}...\n")

    for port in range(start_port, end_port + 1):
        t = threading.Thread(target=scan_port, args=(target, port))
        t.start()

# This line ensures the script runs only when executed directly, not when imported
if __name__ == "__main__":
    main()
