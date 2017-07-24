# ChatApplication
a simple real time chat application written in Flask and utilizing the SOCKET.IO library

example code:

from flask import Flask, render_template
from flask_socketio import SocketIO, send

app = Flask(__name__)
app.config['SECRET_KEY'] = 'mysecret'
socketio = SocketIO(app)


@socketio.on('message')  # listen for a message event
def handlemessage(msg):
    print('Message: ' + msg)
    send(msg, broadcast=True)


@app.route('/chatroom')
def chatroom():
    return render_template('chatroom.html')

if __name__ == '__main__':
    socketio.run(app)    # remember a flask app is used in a typical request-response model with a server involved
    
