GIT_VERSION := $(shell git describe --abbrev=4 --dirty --always --tags)

all: Android.mk rawproxyreverse.c ../libargp/local/armeabi/libargp.a ../libpcap/local/armeabi/libpcap.a FORCE
	touch rawproxyreverse.c
	$(NDK_ROOT)/ndk-build NDK_APPLICATION_MK=`pwd`/Application.mk NDK_APP_OUT=. TARGET_PLATFORM=android-21 GIT_VERSION=$(GIT_VERSION)

../libargp/local/armeabi/libargp.a: FORCE
	cd ../libargp && make

../libpcap/local/armeabi/libpcap.a: FORCE
	cd ../libpcap && make

clean:
	rm -Rf libs
	rm -Rf local

install: libs/armeabi/rawproxyreverse
	adb push $< /sdcard/
	adb shell 'su -c "mount -o rw,remount /system"'
	adb shell 'su -c "cp /sdcard/rawproxyreverse /system/bin/rawproxyreverse"'

FORCE:
