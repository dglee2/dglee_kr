---
title: "OpenBSD ibus-hangul"
date: 2020-08-14
draft: false
tags: ["setup", "OpenBSD", "ibus", "hangul"]
---
대충 기억나는대로 기록해보면... (빠뜨린것 있을수 있음.)

ibus, libhangul은 패키지 인스톨.

github libhangul/ibus-hangul 리포에서 최신 릴리스 소스코드 다운로드.

빌드 환경
* pkg_add autoconf automake gettext-runtime gettext-tools gmake
* AUTOCONF_VERSION, AUTOMAKE_VERSION 환경변수 set.

기본적으로,
```bash
./autogen.sh
./configure
gmake
```

필요시 src/engine.c 수정
```c
288a289
>     gint i;
313c314
<     for (gint i = 0; version_str_array[i] != NULL; ++i) {
---
>     for (i = 0; version_str_array[i] != NULL; ++i) {
```

gettext 버전 mismatch 여서 po 처리가 완료되지 않을때... po 없어도 쓰는덴 상관없어 안해도 되지만, po/Makefile.in.in 수정
```make
10c10,12
< GETTEXT_MACRO_VERSION = 0.19
---
> #GETTEXT_MACRO_VERSION = 0.19
> 
> GETTEXT_MACRO_VERSION = 0.20
```

ibus-hangul PLIST에 따라 빌드 결과물, Python스크립트 설치. (내가 review하지 않은 install 스크립트 돌리기 싫어서 수동으로..) install base는 /usr/local, DATADIR은 /usr/local/share/ibus-hangul 
```
bin/ibus-setup-hangul
libexec/ibus-engine-hangul
libexec/ibus-setup-hangul
share/applications/ibus-setup-hangul.desktop
%%DATADIR%%/data/symbol.txt
%%DATADIR%%/icons/ibus-hangul.png
%%DATADIR%%/icons/ibus-hangul.svg
%%DATADIR%%/setup/config.py
%%DATADIR%%/setup/config.pyc
%%DATADIR%%/setup/config.pyo
%%DATADIR%%/setup/keycapturedialog.py
%%DATADIR%%/setup/keycapturedialog.pyc
%%DATADIR%%/setup/keycapturedialog.pyo
%%DATADIR%%/setup/main.py
%%PYTHON2%%%%DATADIR%%/setup/main.pyc
%%PYTHON2%%%%DATADIR%%/setup/main.pyo
%%DATADIR%%/setup/setup.ui
share/ibus/component/hangul.xml
share/icons/hicolor/64x64/apps/ibus-hangul.png
share/icons/hicolor/64x64/apps/ibus-setup-hangul.png
share/icons/hicolor/scalable/apps/ibus-hangul.svg
share/icons/hicolor/scalable/apps/ibus-setup-hangul.svg
%%NLS%%share/locale/ko/LC_MESSAGES/ibus-hangul.mo
%%NLS%%share/locale/zh_CN/LC_MESSAGES/ibus-hangul.mo
```

ibus-anthy PLIST 참고하여 추가 작업.
```bash
cp data/org.freedesktop.ibus.engine.hangul.metainfo.xml /usr/local/share/metainfo/ 
cp data/org.freedesktop.ibus.engine.hangul.gschema.xml /usr/local/share/glib-2.0/schemas/
glib-compile-schemas /usr/local/share/glib-2.0/schemas
```

한글폰트는... 네이버 나눔폰트 받아서..
/usr/local/share/fonts 아래, Nanum 같은 적당한 이름의 폴더 만들고 아래에다 설치.
