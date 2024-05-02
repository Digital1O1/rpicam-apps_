CC=g++
CFLAGS=-Wall -Wextra -std=c++11 -I/usr/include/rpicam-apps/ -I/home/pi/libcamera/include/ -I/usr/local/include/libcamera/
LDFLAGS=-L/usr/lib/aarch64-linux-gnu -L/home/pi/rpicam-apps/build -lcamera-base -lcamera -lpthread -lcamera_app -lboost_program_options

TARGET=rpicam_still
SRC=rpicam_still.cpp
OBJ=$(SRC:.cpp=.o)

all: $(TARGET)

$(TARGET): $(OBJ)
	$(CC) $(LDFLAGS) $(OBJ) -o $@

.cpp.o:
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) $(TARGET)

# g++ -o rpicam_jpeg /home/pi/rpicam-apps/build/apps/rpicam-jpeg.p/rpicam_jpeg.cpp.o -L/usr/lib/aarch64-linux-gnu -L/home/pi/rpicam-apps/build -lcamera-base -lcamera -lpthread -lcamera_app -lboost_program_options
