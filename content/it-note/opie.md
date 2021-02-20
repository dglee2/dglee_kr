---
title: "OrangePi Debian"
date: 2021-02-20
draft: true
tags: ["OrangePi", "Debian", "Service"]
---
이래서 내가 리눅스 별로 안좋아라 한다. rc 스크립트 들도 그대로 유지하면서 (하위버전 호환성을 위해 그러겠지만..) 거기다 엎쳐서 이젠 systemd 설정도 있네? 시스템 올릴때 두가지 설정을 다 읽어 올리나보다. 중복되는건 어떻게 하는건지는 아직 잘 모르겠지만... 그닥 별 관심도 없고. 아무튼 systemctl 쓰더니 systemd가 관리하는 systemd 시작설정 tree?를 가지고 있네. /etc/systemd/system/ 아래 참조. 그리고 systemctl enable [서비스] 요렇게 enable/disable 시키는것 같다. 뭐냐 이게... rc 스크립트들도 runlevel에 맞춰서 링크걸고 하는게 맘에 안들었는데... 이젠 systemd까지. 덕분에 wpa_supplicant를 systemd 설정에선 뺐는데도 이젠 막 서비스가 올라오고.. 장난아니네.. 누가 시작한건지도 추적이... 되나? 데몬은 부모 버리고 시작하니.. ppid도.. 별 의미 없을테고.. 그리고 이걸 내가 왜 추적해야되지?? ifconfig버리고 ip 로 가는것도 왜? 저걸로 다 되는데.. 안되는건 조금씩 업글하면 되는건데 왜? 싶은데... 아무튼, 리눅스는 너무 난잡하다. bsd는 깔끔하고 효율적인 느낌인데.. 리눅스는 전혀 그렇지 않다.
