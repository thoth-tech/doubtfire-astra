worker_processes 1;

events { }

http {
    include /etc/nginx/mime.types;

    sendfile on;

    # Server block for port 80
    server {
        root /usr/share/nginx/html/;
        index index.html;
        listen 80;

        add_header Content-Security-Policy "default-src https: 'unsafe-inline' 'unsafe-eval' blob: data:" always;
        add_header Feature-Policy "microphone 'self';speaker 'self';fullscreen 'self';payment none;" always;
        add_header Permissions-Policy "microphone=(self), fullscreen=(self), payment=()" always;

        # X-Frame-Options header for clickjacking protection
        add_header X-Frame-Options "DENY" always;
    }

    # Server block for port 4200
    server {
        root /usr/share/nginx/html/;
        index index.html;
        listen 4200;

        add_header Content-Security-Policy "default-src https: 'unsafe-inline' 'unsafe-eval' blob: data:" always;
        add_header Feature-Policy "microphone 'self';speaker 'self';fullscreen 'self';payment none;" always;
        add_header Permissions-Policy "microphone=(self), fullscreen=(self), payment=()" always;

        # X-Frame-Options header for clickjacking protection
        add_header X-Frame-Options "DENY" always;
    }

    # Server block for port 443
    server {
        root /usr/share/nginx/html/;
        index index.html;
        listen 443;

        add_header Content-Security-Policy "default-src https: 'unsafe-inline' 'unsafe-eval' blob: data:" always;
        add_header Feature-Policy "microphone 'self';speaker 'self';fullscreen 'self';payment none;" always;
        add_header Permissions-Policy "microphone=(self), fullscreen=(self), payment=()" always;

        # X-Frame-Options header for clickjacking protection
        add_header X-Frame-Options "DENY" always;
    }
  
    gzip on;
    gzip_types text/css application/javascript;
    gzip_proxied any;
    gzip_buffers 32 8k;
}
