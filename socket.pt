# estas funcoes nao estão implementadas na optica pedida pelo professor
# porque tivemos alguns problemas de implementação 
# nesta versao tem uma simulacao de servidor e de um cliente 
# Andre Edna Fernando
 #imporatar modulodos que seram utilizados
import socket
import threading
import SocketServer
import subprocess

class ThreadedTCPRequestHandler(SocketServer.BaseRequestHandler):

    def handle(self):
        data = self.request.recv(1024)
        cur_thread = threading.current_thread()
        response = "{}: {}".format(cur_thread.name, data)
        self.request.sendall(response)

class ThreadedTCPServer(SocketServer.ThreadingMixIn, SocketServer.TCPServer):
    pass
# funcao que vai receber o IP e a porta do backend 
def receber_do_backend(ip, port, message):
    #  protocolo TCP
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.connect((ip, port))
    try:
        sock.sendall(message)
        response = sock.recv(1024)
        if message == "1" :
            executa_ps = subprocess.Popen("ps",stdout=subprocess.PIPE, shell=True)
            (out_ps,err_ps) = executa_ps.communicate()
            print "program output:", out_ps
        elif message == "2": 
        
            executa_df = subprocess.Popen("df",stdout=subprocess.PIPE, shell=True)
            (out_df,err_df) = executa_df.communicate()
            print "program output:", out_df
        elif message == "3": 
            proc = subprocess.Popen("finger",stdout=subprocess.PIPE, shell=True)
            (out,err) = proc.communicate()
            print "program output:", out
        elif message == "4": 
            proc = subprocess.Popen("uptime",stdout=subprocess.PIPE, shell=True)
            (out,err) = proc.communicate()
            print "program output:", out
       
        print "Received: {}".format(response)
    finally:
        sock.close()

if __name__ == "__main__"8:
    # Port 0 means to select an arbitrary unused port
    HOST, PORT = "localhost", 0

    server = ThreadedTCPServer((HOST, PORT), ThreadedTCPRequestHandler)
    ip, port = server.server_address

    # Start a thread with the server -- that thread will then start one
    # more thread for each request
    server_thread = threading.Thread(target=server.serve_forever)
    # Exit the server thread when the main thread terminates
    server_thread.daemon = True
    server_thread.start()
    print "Server loop running in thread:", server_thread.name
    
    receber_do_backend(ip, port, "1")
    receber_do_backend(ip, port, "2")
    receber_do_backend(ip, port, "3")
    receber_do_backend(ip, port, "4")

    server.shutdown()
    server.server_close()




