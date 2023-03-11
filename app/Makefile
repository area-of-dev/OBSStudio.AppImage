# Copyright 2023 Alex Woroschilow (alex.woroschilow@gmail.com)
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
	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate \
		libavcodec-extra58 libavcodec58 libavutil56 libpython3.8 libswscale5 libswresample3 libavformat58 libavformat58-dev \
		libsndfile1 libavdevice58 libvlc5 \
		libwayland-cursor0 libselinux1  

	rm -rf $(PWD)/build/obsstudio && \
		mkdir --parents $(PWD)/build/obsstudio && \
			git clone --recursive https://github.com/obsproject/obs-studio.git $(PWD)/build/obsstudio

	rm -rf $(PWD)/build/obsstudio/build && \
		mkdir --parents $(PWD)/build/obsstudio/build

	cd $(PWD)/build/obsstudio/build && \
		cmake -DLINUX_PORTABLE=ON -DCMAKE_INSTALL_PREFIX="${PWD}/portable" -DENABLE_NEW_MPEGTS_OUTPUT=OFF -DENABLE_BROWSER=OFF -DENABLE_PIPEWIRE=OFF -DENABLE_AJA=OFF ..

	cd $(PWD)/build/obsstudio/build && \
		make -j4 && make install

	rm --recursive --force $(PWD)/build/Boilerplate.AppDir/data
	rm --recursive --force $(PWD)/build/Boilerplate.AppDir/obs-plugins

	cp --recursive --force ${PWD}/portable/lib/*         $(PWD)/build/Boilerplate.AppDir/lib64/
	cp --recursive --force ${PWD}/portable/bin/*         $(PWD)/build/Boilerplate.AppDir/bin/
	cp --recursive --force ${PWD}/portable/data          $(PWD)/build/Boilerplate.AppDir/data
	cp --recursive --force ${PWD}/portable/obs-plugins   $(PWD)/build/Boilerplate.AppDir/obs-plugins

	rm --recursive --force $(PWD)/build/Boilerplate.AppDir/cmake
	rm --recursive --force $(PWD)/build/Boilerplate.AppDir/include
	rm --recursive --force $(PWD)/build/Boilerplate.AppDir/lib64/libstdc++.so.6*

	echo "LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}:\$${APPDIR}/obs-plugins" >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}:\$${APPDIR}/data" 	    >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ""                                                             >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ""                                                             >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "export LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}" 				    >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "cd \$${APPDIR}/bin/64bit" 		                            >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "./obs \"\$${@}\"" 		                                    >> $(PWD)/build/Boilerplate.AppDir/AppRun

	rm --force $(PWD)/build/Boilerplate.AppDir/*.desktop 		        || true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.png 		  	        || true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.svg 		  	        || true

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
