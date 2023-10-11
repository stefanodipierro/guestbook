FROM golang:1.15 as builder

# Installa le dipendenze
RUN go get github.com/codegangsta/negroni
RUN go get github.com/gorilla/mux 
RUN go get github.com/xyproto/simpleredis/v2

# Copia il codice sorgente nel container
COPY main.go .

# Compila l'applicazione
RUN go build main.go

FROM ubuntu:18.04

# Copia il binario e le risorse nell'immagine finale
COPY --from=builder /go/main /app/guestbook
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

# Imposta la directory di lavoro
WORKDIR /app

# Imposta il comando di esecuzione dell'applicazione
CMD ["./guestbook"]

# Espone la porta 3000
EXPOSE 3000
