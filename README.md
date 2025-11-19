3-3_Restore_Svc_Role
============================================
이 역할에 대한 설명 작성.
============================================
이 역할은 웹 서비스 복구를 위한 롤백 작업을 수행.
방화벽에서 웹 관련 포트를 차단하고,
관련 서비스를 중지 및 비활성화하며,
웹 관련 파일과 패키지를 제거하는 작업을 수행.

Requirements
============================================
이 역할은 Ansible 자체의 기본 기능을 사용하므로 별도의 사전 요구 사항은 없음.
단, firewalld, systemd, dnf 모듈이 시스템에 필수 설치가 전제 조건.

Role Variables
============================================
변수명	 / 설명	                                              / 기본값
fw_svc / 방화벽에서 차단할 서비스 목록 (HTTP/HTTPS 등)	        / http, https
svcs   / 중지 및 비활성화할 서비스 목록 (httpd, firewalld 등)	/ httpd, firewalld
files  / 삭제할 웹 인덱스 파일 목록	                          / /var/www/html/index.html
pkgs	 / 제거할 패키지 목록

Dependencies
============================================
이 역할은 외부 역할이나 의존성 없이 단독으로 사용 가능.
firewalld, systemd, dnf 모듈을 사용하므로, 해당 모듈이 시스템에 설치되어 있어야 함.

Example Playbook
============================================
이 역할을 사용하려면 다음과 같은 플레이북 예시를 참고.
- hosts: servers
  roles:
    - role: rollback-svc
      fw_svc:
        - http
        - https
      svcs:
        - httpd
        - firewalld
      files:
        - /var/www/html/index.html
      pkgs:
        - httpd
      
License
============================================
BSD License

Author Information
============================================
진성은
