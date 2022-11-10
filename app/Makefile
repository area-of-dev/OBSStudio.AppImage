# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
PWD:=$(shell pwd)

.PHONY: all

all: clean init
	mkdir --parents $(PWD)/build/Boilerplate.AppDir

	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate obs-studio ffmpeg x264 \
		xdg-desktop-portal xdg-desktop-portal-gtk xdg-desktop-portal-kde pipewire-media-session qtwayland5 qt5-wayland \
	    libgdk-pixbuf2.0-0 libatk1.0-0 libatk-bridge2.0-0 libgtk2.0-0 \
	    libreadline8 at-spi2-core libpango-1.0-0 libgtk-3-0 \
		libwayland-cursor0 libselinux1 

	sed -i -e 's|../../obs-plugins/64bit|././././lib/obs-plugins|g' $(PWD)/build/Boilerplate.AppDir/lib64/libobs.so.0

	echo ''                            >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                            >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'cd $${APPDIR}'               >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo '$${APPDIR}/bin/obs "$${@}"'  >> $(PWD)/build/Boilerplate.AppDir/AppRun

	rm --force $(PWD)/build/Boilerplate.AppDir/*.desktop 		      || true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.png 		  	      || true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.svg 		  	      || true
	rm --force $(PWD)/build/Boilerplate.AppDir/lib64/libstdc++.so.6*  || true

	cp --force $(PWD)/AppDir/*.desktop  $(PWD)/build/Boilerplate.AppDir/ || true
	cp --force $(PWD)/AppDir/*.png      $(PWD)/build/Boilerplate.AppDir/ || true
	cp --force $(PWD)/AppDir/*.svg      $(PWD)/build/Boilerplate.AppDir/ || true

	export ARCH=x86_64 && $(PWD)/bin/appimagetool.AppImage $(PWD)/build/Boilerplate.AppDir $(PWD)/OBSStudio.AppImage
	chmod +x $(PWD)/OBSStudio.AppImage

init:
	mkdir --parents $(PWD)/bin

	wget https://apprepo.de/appimage/download/apprepo \
		--output-document=$(PWD)/bin/Apprepo.AppImage
	chmod +x $(PWD)/bin/Apprepo.AppImage

	wget https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage \
		--output-document=$(PWD)/bin/appimagetool.AppImage
	chmod +x $(PWD)/bin/appimagetool.AppImage

clean:
	rm -rf $(PWD)/*.AppImage
	rm -rf $(PWD)/bin/*
	rm -rf $(PWD)/build
