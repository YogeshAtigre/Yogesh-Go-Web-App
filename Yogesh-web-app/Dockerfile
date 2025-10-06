# Stage 1 of the Multi Stage Docker file 

FROM golang:1.22 AS builder

# Setting up the working directory

WORKDIR /app

# Copying the Additional requirements 
# It is similar to pip install -r requirements.txt 

COPY go.mod ./

RUN go mod download

# Copying the sources code into the working dir

COPY . .

# Buliding the app

RUN go build -o main .

# Stage 2 Only coyping and building the rquired files

# We will use a distroless image to run the application

FROM gcr.io/distroless/base


# copying the source code from builder stage
COPY --from=builder /app/main .

# Copying the static files 
COPY --from=builder /app/static ./static

# Exposing the port on which the app will run 
EXPOSE 8060

CMD [ "./main" ]
