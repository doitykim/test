---

- **목차**

---

지금쯤은 Ansible이 시스템 관리자 작업을 자동화하는 데 뛰어난 도구라는 것을 이해하고 있을 것입니다. 이 장에서는 VMware 인프라에 중점을 두고 있습니다. 시간을 절약하고 오류를 줄이기 위한 일상적인 사용 사례를 공유할 것입니다. 다음 페이지에서는 VMware 인프라를 자동화하기 위해 가장 중요한 Ansible 모듈과 플러그인에 대해 배울 것입니다. VMware 데이터 센터, 클러스터, 호스트 시스템, 그리고 가상 머신과 상호작용하는 코드도 포함되어 있습니다. 이 장이 끝나면, 몇 줄의 코드로 가상 머신을 생성하거나 두 번째 하드 드라이브를 추가하는 등 일상적인 작업을 자동화할 수 있게 될 것입니다.

[VMware Guide — Ansible Documentation](https://docs.ansible.com/ansible/6/collections/community/vmware/docsite/scenario_guide.html)

# [**01. VMware 자동화를 위한 Ansible 구성하기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 인프라와 상호작용하기 위한 모든 Ansible 리소스는 Ansible 컬렉션 `community.vmware`에 포함되어 있습니다. 이 리소스들은 Ansible과 마찬가지로 Python으로 작성되어 있으며, 실행을 위해서 일부 Python 의존성(dependency)이 필요합니다. 컬렉션의 주요 의존성은 `pyVmomi`로, 이는 VMware vSphere API를 위한 Python SDK로 VMware ESX, ESXi 및 vCenter 인프라에 연결하고 관리할 수 있게 해줍니다. 각 Ansible 모듈은 VMware 인프라의 특정 요소(데이터 센터, 클러스터, 호스트 시스템, 가상 머신)와 상호작용합니다. Ansible 컨트롤러를 VMware 인프라와 상호작용할 수 있도록 준비하는 방법을 단계별로 보여드리겠습니다. 이 초기 구성은 일부 VMware 사용자들에게 Ansible을 시작하는 데 장애물이 될 수 있습니다.

VMware 오류에 대한 가장 일반적인 Ansible 문제를 해결하고 해결하는 방법은 다음 섹션을 참조하십시오:

- **VMware failed to import pyVmomi**
- **VMware unknown error while connecting to vCenter or ESXi**
- **VMware certificate verification failed connecting to vCenter or ESXi**

## **The Ansible vmware.vmware_rest Collection**

`vmware.vmware_rest` Ansible 컬렉션은 `community.vmware` 컬렉션의 대안으로, VMware vSphere REST API 인터페이스를 기반으로 하며 `pyVmomi` 및 vSphere Automation SDK for Python과 같은 서드파티 라이브러리에 의존하지 않습니다. 대신, Python 3.6 이상에서는 `aiohttp` Python 라이브러리가 필요합니다.

이 책을 집필하는 시점에서 `vmware.vmware_rest` 컬렉션은 VMware 가상 머신의  life cycle과 VMware vCenter 서버 어플라이언스(VCSA) 자동화 리소스 관리에만 중점을 두고 있습니다.

이 컬렉션은 Ansible VMware 커뮤니티에 의해 지원되며, VMware 인프라 관리를 돕기 위한 VMware 모듈과 플러그인을 포함하고 있지만 현재는 제한된 자동화 옵션만을 제공합니다.

자세한 사항은 https://docs.ansible.com/ansible/latest/collections/vmware/vmware_rest/docsite/guide_vmware_rest.html 사이트 문서를 참조하세요.

이 책에서는 현재 더 많은 자동화 리소스를 제공하는 `community.vmware` 컬렉션을 다루고 있습니다.

## **The Ansible community.vmware Collection**

[Community.Vmware — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/collections/community/vmware/index.html)

- **VMware vSphere 8.0, 7.0, 6.0, 5.5, 5.1 and 5.0**

지원되는 노드에는 VMware vSphere의 최신 릴리스가 모두 포함됩니다. 전체 목록에는 vSphere의 최신 릴리스와 8.0, 7.0, 6.0, 5.5, 5.1 및 5.0이 포함됩니다. Ansible community.vmware VMware 컬렉션에는 Python pyVmomi 라이브러리가 필요합니다. pyVmomi는 VMware vSphere API와 상호 작용하는 소프트웨어 개발 키트(SDK)로, ESX, ESXi 및 vCenter 인프라를 관리하여 Ansible 자동화를 실행할 수 있습니다.

- **Python pyVmomi supports 2.7.x and 3.4+**
- **Ansible collection community.vmware**

Ansible collection community.vmware에는 VMware 인프라에서 모든 작업과 작업을 수행할 수 있는 유용한 자동화 기능이 포함된 모듈과 플러그인이 포함되어 있습니다(174개).  진화하는 컬렉션이므로 공식 문서를 살펴보는 것을 고려하십시오. community.vmware Ansible collection은 이름에서 알 수 있듯이 커뮤니티 지원에 의해 제공되므로 앤서블 엔지니어 팀이 직접 유지 관리하지는 않습니다. ommunity-supported 컬렉션은 자원봉사자 앤서블 개발자와 크리에이터의 최선의 지원을 받습니다. 오픈 소스 정신에 따라 얼마든지 기여할 수 있습니다.

### **Links**

- **Introduction to Ansible for VMware**
https://docs.ansible.com/ansible/6/collections/community/vmware/docsite/vmware_scenarios/vmware_intro.html
- **Plugin Index.Modules**
https://docs.ansible.com/ansible/latest/collections/community/vmware/index.html#plugin-index

### **Code**

VMware 인프라를 자동화하기 위한 주요 세 가지 단계를 안내해 드리겠습니다. Ansible 여정을 성공적으로 시작할 수 있도록 관련된 모든 자료를 공유하겠습니다. Ansible Playbook을 사용하여 VMware 가상 머신에 대한 정보를 수집하는 사용 사례를 고려해 보겠습니다. VMware를 위한 Ansible 설정 방법은 다음과 같습니다:

1. **Install pyVmomi.**
2. **Install the community.vmware collection.**
3. **Ansible code, inventory, and Playbook**

1. **Install pyVmomi**

먼저, VMware vSphere API Python 바인딩인 pyVmomi를 설치해야 합니다.

필수 pyVmomi Python 라이브러리가 없는 시스템에서 Ansible Playbook을 처음 실행하려고 할 때 치명적인 오류가 발생할 것입니다. 이 오류는 Ansible이 현재 Python 가상 환경이나 Ansible 실행 환경에서 Python 라이브러리를 찾지 못한다는 것을 나타낼 수도 있습니다. pyVmomi Python 라이브러리가 없을 때마다 실행이 FAILED 상태로 종료되며, 다음과 같은 **fatal error**와 설명이 표시됩니다:

```yaml
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: ModuleNotFoundError: No module named 'pyVim'
"Failed to import the required Python library (pyVmomi ) on demo.example.com's Python /usr/libexec/platform-python. Please read module documentation and install in the appropriate location. If the required library is installed, but Ansible is using the wrong Python interpreter, please consult the documentation on ansible_python_interpreter"
```

필요한 pyVmomi Python 라이브러리는 Python 패키지 관리자(PIP)를 사용하여 설치할 수 있습니다. 시스템에서 실행 중인 Python 버전에 따라 명령어를 조정해야 할 수도 있습니다. 예를 들어, Python 3의 경우 pip3, Python 3.9의 경우 pip3.9을 사용합니다. 일부 배포판에서는 python3-pip 패키지 설치가 필요할 수 있습니다. 다음 명령어는 **root** 권한을 사용하여 시스템 전체에 pyVmomi Python 라이브러리를 설치합니다:

```bash
sudo pip install pyVmomi
```

PIP는 requests, six, chardet, idna, urllib3와 같은 필요한 모든 Python 종속성을 처리합니다.

이 명령어를 실행한 후에는 pyVmomi가 시스템에 성공적으로 설치되어 다음 단계로 진행할 준비가 됩니다.

1. **Install the community.vmware collection**

둘째, Ansible `community.vmware` 컬렉션을 설치해야 합니다. 가장 좋은 Ansible 방법은 `requirements.yml` 파일을 사용하는 것입니다. ansible-galaxy 명령어를 사용하여 수동으로 설치할 수도 있지만, 저는 워크플로우를 최대한 자동화하는 것을 선호합니다. 이 코드는 스크립트나 Ansible Playbook에 삽입할 수도 있습니다. Ansible `requirements.yml` 파일을 사용하면 설치하려는 모든 Ansible 컬렉션 또는 Ansible Role을 지정할 수 있습니다. 이번 사용 사례에서는 community.vmware 컬렉션 이름을 포함한 간단한 YAML 문서입니다.

> **requirements.yml**
> 

```yaml
---
collections:
  - name: community.vmware
```

다음 명령어로 컬렉션을 설치할 수 있습니다:

```bash
ansible-galaxy install -r requirements.yml
```

이 명령어를 실행한 후에는 community.vmware 컬렉션이 시스템에 성공적으로 설치되며, Ansible 코드를 완전히 실행할 준비가 됩니다.

1. **Ansible code, inventory, and Playbook**

모든 작업이 노드에서 완료되면, Ansible 컨트롤러 머신에서 Ansible 인벤토리를 구성하고 `vmware_guest_info` 모듈을 사용하여 첫 번째 Ansible Playbook을 실행하여 구성의 성공 여부를 확인할 수 있습니다.

Ansible 인벤토리는 매우 간단하며, Ansible 컨트롤러가 VMware API를 통해 VMware 인프라에 연결할 것이기 때문에 `localhost`로 제한됩니다.

> **Inventory**
> 

```
[local]
localhost ansible_connection=local
```

`vm_info.yml` Ansible Playbook은 단순히 VMware 인프라에서 VMware 가상 머신의 세부 정보를 수집하고 화면에 출력합니다. Ansible Playbook 내부에서 사용되는 변수들은 `vars.yml` 파일에 정의되어 있습니다. 이 테스트는 VMware 인프라에 연결하고, VMware API에 가상 머신 이름이라는 매개변수를 사용하여 정보를 요청하고, JSON 형식으로 정보를 반환하는 좋은 방법입니다. 이 정보를 처리하여 추가 자동화를 실행하거나, 이 예제처럼 화면에 출력할 수 있습니다.

> **vm_info.yml**
> 

```yaml
---
- name: info vm demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: get VM info
      vmware_guest_info:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
      register: detailed_vm_info
    - name: print VM info
      ansible.builtin.debug:
        var: detailed_vm_info
```

모든 연결 매개변수를 별도의 vars.yml 파일에 저장하여 다른 Ansible Playbook 파일들 간에 공유하는 것이 좋습니다. 이 문서에는 VMware 인프라에 연결하기 위한 사용자 이름과 비밀번호가 포함되어 있으므로, Ansible Vault를 사용하여 이 문서를 암호화할 것을 강력히 권장합니다.

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-AD-50.253-tanzukr.com"
```

다음은 Ansible Playbook에서 사용되는 간단한 변수들로, 실제로 VMware 인프라에서 사용하는 값으로 맞추어야 합니다.

- `vcenter_hostname`은 VMware ESXi 또는 vCenter의 호스트 이름이나 IP 주소를 포함합니다.
- `vcenter_datacenter`는 데이터 센터의 이름을 포함하며, 예를 들어 **`LvDC`**가 될 수 있습니다.
- `vcenter_validate_certs`는 SSL 인증서 검증을 활성화(`true`)하거나 비활성화(`false`)하는 부울 값입니다. 저는 인프라에서 자체 서명된 인증서를 사용하기 위해 SSL 인증서 검증을 비활성화했습니다. 유효한 SSL 인증서를 사용하거나 로컬 인증 기관을 시스템의 신뢰 체인에 삽입하는 것을 권장합니다.
- `vcenter_username`은 VMware 인프라에 연결하기 위한 사용자 이름을 포함합니다. 로컬 사용자 이름인 경우 접미사로 `@vsphere.local`을 추가하거나 LDAP/ActiveDirectory 자격 증명을 사용해야 합니다.
- `vcenter_password`는 연결에 사용되는 비밀번호를 포함합니다. 대소문자 및 특수 문자에 주의하십시오. 일부 문자는 Ansible에서 사용할 때 이스케이프해야 할 수도 있습니다.
- `vm_name`은 정보를 얻고자 하는 가상 머신의 이름을 포함합니다. 이 예제에서는 **`shim-AD-50.253-tanzukr.com`**입니다.

코드를 자유롭게 커스터마이즈하거나 명령줄에서 추가 변수를 사용하십시오.

```yaml
ansible-playbook vm_info.yml
```

- **실행결과**
    
    ```yaml
    [iradmin@ansible-master Configure Ansible For VMware]$ ansible-playbook vm_info.yml 
    [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
    
    PLAY [info vm demo] ****************************************************************************************************************
    
    TASK [include_vars] ****************************************************************************************************************
    ok: [localhost]
    
    TASK [get VM info] *****************************************************************************************************************
    ok: [localhost]
    
    TASK [print VM info] ***************************************************************************************************************
    ok: [localhost] => {
        "detailed_vm_info": {
            "changed": false,
            "failed": false,
            "instance": {
                "advanced_settings": {
                    "RemoteDisplay.maxConnections": "-1",
                    "cpuid.coresPerSocket": "2",
                    "disk.EnableUUID": "TRUE",
                    "ethernet0.pciSlotNumber": "192",
                    "guestInfo.detailed.data": "architecture='X86' bitness='64' buildNumber='17763' distroName='Windows' distroVersion='10.0' familyName='Windows' kernelVersion='17763.5576' prettyName='Windows Server 2019, 64-bit (Build 17763.5576)'",
                    "guestinfo.Cb.InstallStatus": "3013",
                    "guestinfo.Cb.LauncherVersion": "1.1.0",
                    "guestinfo.driver.vmci.version": "9.8.18.0",
                    "guestinfo.driver.vsock.version": "9.8.19.0",
                    "guestinfo.driver.wddm.version": "9.17.04.0002",
                    "guestinfo.vmtools.buildNumber": "20735119",
                    "guestinfo.vmtools.description": "VMware Tools 12.1.5 build 20735119",
                    "guestinfo.vmtools.versionNumber": "12325",
                    "guestinfo.vmtools.versionString": "12.1.5",
                    "guestinfo.vmware.components.available": "salt_minion",
                    "hpet0.present": "TRUE",
                    "migrate.hostLog": "shim-AD-50.253-tanzukr.com-0c298a4e.hlog",
                    "migrate.hostLogState": "none",
                    "migrate.migrationId": "0",
                    "monitor.phys_bits_used": "45",
                    "numa.autosize.cookie": "40022",
                    "numa.autosize.vcpu.maxPerVirtualNode": "4",
                    "nvram": "shim-AD-50.253-tanzukr.com.nvram",
                    "pciBridge0.pciSlotNumber": "17",
                    "pciBridge0.present": "TRUE",
                    "pciBridge4.functions": "8",
                    "pciBridge4.pciSlotNumber": "21",
                    "pciBridge4.present": "TRUE",
                    "pciBridge4.virtualDev": "pcieRootPort",
                    "pciBridge5.functions": "8",
                    "pciBridge5.pciSlotNumber": "22",
                    "pciBridge5.present": "TRUE",
                    "pciBridge5.virtualDev": "pcieRootPort",
                    "pciBridge6.functions": "8",
                    "pciBridge6.pciSlotNumber": "23",
                    "pciBridge6.present": "TRUE",
                    "pciBridge6.virtualDev": "pcieRootPort",
                    "pciBridge7.functions": "8",
                    "pciBridge7.pciSlotNumber": "24",
                    "pciBridge7.present": "TRUE",
                    "pciBridge7.virtualDev": "pcieRootPort",
                    "sata0.pciSlotNumber": "32",
                    "sched.cpu.latencySensitivity": "normal",
                    "sched.swap.derivedName": "/vmfs/volumes/6b9a781d-8825837f/shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com-65e05f70.vswp",
                    "scsi0.pciSlotNumber": "160",
                    "scsi0.sasWWID": "50 05 05 6b c1 2a 88 e0",
                    "scsi0:0.redo": "",
                    "softPowerOff": "FALSE",
                    "svga.guestBackedPrimaryAware": "TRUE",
                    "svga.present": "TRUE",
                    "tools.guest.desktop.autolock": "TRUE",
                    "tools.remindInstall": "FALSE",
                    "toolsInstallManager.lastInstallError": "0",
                    "toolsInstallManager.updateCounter": "1",
                    "usb_xhci.pciSlotNumber": "224",
                    "usb_xhci:4.parent": "-1",
                    "usb_xhci:4.port": "4",
                    "viv.moid": "bf2b2c5a-4cf8-4cdb-9e68-be43bf4b5d85:vm-2011:a1h2l5iRd6ksD+AIXO3XZYXse06SteP1V2SSoEuoumE=",
                    "vm.genid": "7873981598851227530",
                    "vm.genidX": "4116818600639604326",
                    "vmotion.checkpointFBSize": "4194304",
                    "vmotion.checkpointSVGAPrimarySize": "8388608",
                    "vmotion.svga.graphicsMemoryKB": "8192",
                    "vmotion.svga.mobMaxSize": "8388608",
                    "vmware.tools.internalversion": "12325",
                    "vmware.tools.requiredversion": "12384",
                    "vmxstats.filename": "shim-AD-50.253-tanzukr.com.scoreboard"
                },
                "annotation": "",
                "current_snapshot": {
                    "creation_time": "2023-04-17T07:22:21.764834+00:00",
                    "description": "",
                    "id": 2,
                    "name": "Installed DNS DHCP",
                    "quiesced": false,
                    "state": "poweredOn"
                },
                "customvalues": {},
                "guest_consolidation_needed": false,
                "guest_question": null,
                "guest_tools_status": "guestToolsRunning",
                "guest_tools_version": "12325",
                "hw_cluster": "LvCL",
                "hw_cores_per_socket": 2,
                "hw_datastores": [
                    "NETAPP_CA",
                    "NETAPP_ISO"
                ],
                "hw_esxi_host": "vl01.lab.iroo.int",
                "hw_eth0": {
                    "addresstype": "assigned",
                    "ipaddresses": [
                        "192.168.50.253"
                    ],
                    "label": "Network adapter 1",
                    "macaddress": "00:50:56:b1:fd:f2",
                    "macaddress_dash": "00-50-56-b1-fd-f2",
                    "portgroup_key": "dvportgroup-226",
                    "portgroup_portkey": "261",
                    "summary": "DVSwitch: 50 34 bf 0b 69 5d 60 b7-a7 58 a3 4a 9e 95 cf 5e"
                },
                "hw_files": [
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmx",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com-Snapshot1.vmsn",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com-Snapshot2.vmsn",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmxf",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.nvram",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmsd",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-239.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-238.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-0.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-237.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-241.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-240.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-243.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-242.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-245.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-244.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-246.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware.log",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1.vmdk",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1-000001.vmdk",
                    "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1-000002.vmdk"
                ],
                "hw_folder": "/LvDC/vm/CA/shim/MGMT",
                "hw_guest_full_name": "Microsoft Windows Server 2019 (64-bit)",
                "hw_guest_ha_state": null,
                "hw_guest_id": "windows2019srv_64Guest",
                "hw_interfaces": [
                    "eth0"
                ],
                "hw_is_template": false,
                "hw_memtotal_mb": 16384,
                "hw_name": "shim-AD-50.253-tanzukr.com",
                "hw_power_status": "poweredOn",
                "hw_processor_count": 4,
                "hw_product_uuid": "4231fa4b-c12a-88ef-2894-0ac9a9c7d0ed",
                "hw_version": "vmx-17",
                "instance_uuid": "5031cd1e-14a0-8f1f-3482-b0b78a8b5c27",
                "ipv4": "192.168.50.253",
                "ipv6": null,
                "module_hw": true,
                "moid": "vm-2011",
                "snapshots": [
                    {
                        "creation_time": "2023-04-17T07:06:05.007092+00:00",
                        "description": "",
                        "id": 1,
                        "name": "Installed DNS",
                        "quiesced": false,
                        "state": "poweredOn"
                    },
                    {
                        "creation_time": "2023-04-17T07:22:21.764834+00:00",
                        "description": "",
                        "id": 2,
                        "name": "Installed DNS DHCP",
                        "quiesced": false,
                        "state": "poweredOn"
                    }
                ],
                "tpm_info": {
                    "provider_id": null,
                    "tpm_present": false
                },
                "vimref": "vim.VirtualMachine:vm-2011",
                "vnc": {}
            }
        }
    }
    
    PLAY RECAP *************************************************************************************************************************
    localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    
    ```
    
    이전 단계가 성공적으로 완료되면, Ansible 실행이 매우 매끄럽게 진행되며 화면에서 `shim-AD-50.253-tanzukr.com` 가상 머신의 모든 세부 정보를 확인할 수 있습니다.
    
    가장 중요한 핵심은 VMware 가상 머신에 대한 모든 관련 정보를 읽을 수 있는 인스턴스입니다.
    
    - Running server: "hw_esxi_host": "vl01.lab.iroo.int"
    - Running cluster: "hw_cluster": "LvCL"
    - Virtual machine name: "hw_name": "shim-AD-50.253-tanzukr.com"
    - Motion id: "moid": "vm-2011"
    - Instance UUID: "hw_product_uuid": "4231fa4b-c12a-88ef-2894-0ac9a9c7d0ed"
    - Number of CPU processors: "hw_processor_count": 4
    - Number of CPU cores: "hw_cores_per_socket": 2
    - RAM resources: "hw_memtotal_mb": 16384
    - Datastore name:
        
        ```yaml
        "hw_datastores": [
                        "NETAPP_CA",
                        "NETAPP_ISO"
                    ]
        ```
        
    - Datastore directory: "hw_folder": "/LvDC/vm/CA/shim/MGMT"
    - Datastore files:
        
        ```yaml
        "hw_files": [
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmx",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com-Snapshot1.vmsn",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com-Snapshot2.vmsn",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmxf",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.nvram",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com.vmsd",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-239.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-238.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-0.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-237.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-241.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-240.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-243.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-242.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-245.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-244.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware-246.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/vmware.log",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1.vmdk",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1-000001.vmdk",
                        "[NETAPP_CA] shim-AD-50.253-tanzukr.com/shim-AD-50.253-tanzukr.com_1-000002.vmdk"
                    ],
        ```
        
    - Network interfaces and status:
        
        ```yaml
        "hw_eth0": {
                        "addresstype": "assigned",
                        "ipaddresses": [
                            "192.168.50.253"
                        ],
                        "label": "Network adapter 1",
                        "macaddress": "00:50:56:b1:fd:f2",
                        "macaddress_dash": "00-50-56-b1-fd-f2",
                        "portgroup_key": "dvportgroup-226",
                        "portgroup_portkey": "261",
                        "summary": "DVSwitch: 50 34 bf 0b 69 5d 60 b7-a7 58 a3 4a 9e 95 cf 5e"
                    },
        ```
        
    - Status of VMware Guest Tools:
        
        ```yaml
        "guest_tools_status": "guestToolsRunning"
        ```
        

이제 VMware vSphere 사용자 인터페이스나 복잡한 VMware API와의 추가적인 상호작용 없이 VMware 인프라에 대해 어떤 Ansible 자동화든 실행할 수 있습니다. 공식적으로 Ansible을 활용한 VMware 인프라 자동화의 첫걸음을 내딛게 된 것입니다. 아마도 매일 반복해서 실행하는 가장 지루한 작업을 자동화할 방법에 대해 이미 고민하고 계실 것입니다.

# [**02. Python 가상환경 구성하기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Python 가상 환경을 사용하는 것은 운영 체제에 영향을 주지 않고 VMware를 위한 Ansible 리소스를 활용하는 편리한 방법입니다. 최신 릴리스나 특정 버전의 리소스를 사용할 때 유용하며, 운영 체제와의 충돌 없이 `community.vmware` Ansible 컬렉션과 관련된 Python 라이브러리의 의존성을 관리하는 데에도 좋습니다. Python 가상 환경은 Python이 생성하는 제한된 공간으로, 특정 버전의 Python 라이브러리와 리소스를 사용할 수 있습니다.

Ansible VMware `community.vmware` 컬렉션을 위해 Python 3.8의 최신 릴리스와 최신 `pyVmomi` 및 VMware vSphere Automation SDK for Python 라이브러리를 사용할 수 있도록 Python 가상 환경을 구성하세요. 이 초기 설정은 일부 VMware 사용자에게 Ansible 사용을 시작하는 데 있어 장애물이 될 수 있습니다.

### **Links**

- **Ansible collection community.vmware https://docs.ansible.com/ansible/latest/collections/community/vmware/index.html**
- **Python pyVmomi https://github.com/vmware/pyvmomi**
- **VMware vSphere Automation SDK for Python https://github.com/vmware/vsphere-automation-sdk-python**

### **Code**

ESXi 또는 vCenter 서버에서 가상 머신과 관련된 다양한 작업을 관리하기 위해 `community.vmware` Ansible 컬렉션의 모듈과 플러그인을 성공적으로 사용하려면 Python 가상 환경을 구성할 수 있습니다. Ansible VMware를 위해 Python 가상 환경에서 처리해야 하는 두 가지 주요 Python 의존성은 다음과 같습니다:

1. **pyVmomi**: VMware vSphere API를 Python으로 사용할 수 있게 해주는 라이브러리입니다. VMware 인프라와의 상호작용을 가능하게 합니다.
2. **vsphere-automation-sdk-python**: VMware vSphere Automation SDK for Python

Ansible For VMware 리소스는 VMware vSphere API를 위한 pyVmomi Python SDK 위에서 작성되어, ESX, ESXi 및 vCenter 인프라를 관리할 수 있게 해줍니다. 또 다른 유용한 라이브러리는 VMware vSphere Automation SDK for Python으로, Ansible 동적 인벤토리 `vmware_vm_inventory` 플러그인에서 태그 목록을 나열하는 등의 추가 기능을 제공하는 데 사용됩니다. 이 예제는 Python 3.8을 사용하므로 `pip3.8` 도구가 현재 구성에 맞게 조정됩니다. 일부 Linux 배포판에서는 PIP 도구를 제공하기 위해 `python-pip` 또는 `python3-pip` 패키지를 설치해야 합니다. 시스템에서 실행 중인 버전에 따라 `python3.8`을 `python`, `python3`, `python3.9`로, `pip3.8`을 `pip`, `pip3`, `pip3.9`로 조정하십시오.

> **configure-Python-venv.sh**
> 

```yaml
#!/bin/bash
python3.9 -m venv venv
source venv/bin/activate
pip3.9 install --upgrade pip setuptools
pip3.9 install --upgrade pyvmomi
pip3.9 install --upgrade git+https://github.com/vmware/vsphere-automation-sdk-python.git
```

첫 번째 명령어는 Python 모듈 `venv`를 사용하여 `venv`라는 이름의 새로운 Python 가상 환경을 초기화합니다. 이름은 필요에 따라 변경할 수 있지만, `venv/bin/activate`의 활성화 스크립트에서 `venv` 부분도 그에 맞게 변경해야 합니다. 언제든지 `deactivate` 명령어를 입력하여 가상 환경을 종료할 수 있습니다. Python 가상 환경 이름(venv)이 대괄호 안에 표시된 프롬프트 변경은 실제로 `venv` Python 가상 환경 안에서 작업하고 있음을 확인하는 일반적인 방법입니다.

좋은 방법 중 하나는 PIP 패키지 관리자를 최신 버전으로 업그레이드하고, 패키지 설치를 쉽게 관리할 수 있는 도구를 설정한 다음 Python 리소스를 설치하는 것입니다. 이 경우, `pyVmomi`와 `vsphere-automation-sdk-python` Python 라이브러리가 설치됩니다.

PIP 패키지 설치 관리자는 다음과 같은 모든 필요한 Python 종속성을 처리합니다:

- **`requests`**: HTTP 요청을 처리하는 데 사용되는 라이브러리입니다.
- **`six`**: Python 2와 3 간의 호환성을 제공하는 라이브러리입니다.
- **`chardet`**: 문자 인코딩을 감지하는 데 사용되는 라이브러리입니다.
- **`idna`**: 국제 도메인 이름(Internationalized Domain Names, IDN)을 지원하는 라이브러리입니다.
- **`urllib3`**: HTTP 요청을 처리하기 위한 고급 라이브러리입니다.

이 종속성들은 `pyVmomi`와 `vsphere-automation-sdk-python` 라이브러리의 설치와 작동에 필수적입니다.

설치가 완료되면, 다른 시스템과 공유하거나 Python 가상 환경을 재생성하는 데 유용한 `requirements.txt` 파일을 생성할 수 있습니다. 이 파일을 생성하려면 다음 명령어를 사용합니다:

```bash
pip3.9 freeze > requirements.txt
```

이 명령어는 현재 가상 환경에 설치된 모든 패키지와 그 버전 정보를 `requirements.txt` 파일에 기록합니다. 이후 이 파일을 사용하여 동일한 환경을 다른 시스템에서 재구성하거나 가상 환경을 새로 만드는 데 활용할 수 있습니다.

> **requirements.txt**
> 

```yaml
ansible==7.7.0
ansible-core==2.14.14
Brlapi==0.8.2
cffi==1.14.5
chardet==4.0.0
chrome-gnome-shell==0.0.0
cryptography==36.0.1
cupshelpers==1.0
dasbus==1.4
dbus-python==1.2.18
distro==1.5.0
file-magic==0.4.0
gpg==1.15.1
idna==2.10
libcomps==0.1.18
lxml==4.6.5
nftables==0.1
packaging==20.9
perf==0.1
pexpect==4.8.0
ply==3.11
psutil==5.8.0
ptyprocess==0.6.0
pycairo==1.20.1
pycparser==2.20
pycups==2.0.1
pycurl==7.43.0.6
PyGObject==3.40.1
pyparsing==2.4.7
PySocks==1.7.1
python-dateutil==2.8.1
python-linux-procfs==0.7.0
pyudev==0.22.0
pyvmomi==8.0.3.0.1
PyYAML==5.4.1
requests==2.25.1
resolvelib==0.5.4
rpm==4.16.1.3
selinux==3.5
sepolicy==3.5
setools==4.4.1
setroubleshoot==3.3.31
six==1.15.0
sos==4.5.1
systemd-python==234
urllib3==1.26.5
```

# [**03. VM 생성하기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible Playbook과`vmware_guest` 모듈을 사용하여 VMware 가상 머신 게스트를 자동으로 생성을 실행할 수 있습니다. VMware 가상 머신을 생성하는 작업은 시스템 관리자에게 가장 일상적인 작업 중 하나입니다. 또한, 전통적으로 VMware vSphere 사용자 인터페이스에서 일부 인간의 상호작용이 필요하기 때문에 오류가 발생하기 쉬운 작업입니다.

전통적인 가상 머신 생성 방법은 vSphere 클라이언트 또는 웹 사용자 인터페이스에서 몇 가지 양식을 작성하는 것을 요구합니다. 이 양식들은 다양한 사용 사례를 염두에 두고 설계되었기 때문에 옵션이 매우 많아서 초보자들에게 복잡하게 느껴질 수 있습니다.

예를 들어, 64비트 운영 체제를 실행하는 Linux 가상 머신을 생성하고 다음과 같은 자원을 할당해 보겠습니다: 1개의 CPU, 1GB의 RAM, 10GB의 Thin 프로비저닝된 스토리지.

![Screenshot 2024-07-29 at 10.36.06 AM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/25394990-94ac-4c0f-be69-e3f89a62c2e1/Screenshot_2024-07-29_at_10.36.06_AM.png)

## **Ansible vmware_guest Module**

- **community.vmware.vmware_guest**

Ansible 모듈 `vmware_guest`는 VMware 인프라와 상호작용하여 VMware 가상 머신을 생성하거나 관리하는 데 사용됩니다. 전체 이름은 `community.vmware.vmware_guest`이며, 이는 VMware와 상호작용하는 모듈 모음의 일부로 커뮤니티 지원을 받는 모듈임을 의미합니다. `vmware_guest` 모듈은 VMware vSphere 가상 머신을 생성하기 위해 모든 필요를 맞출 수 있는 매우 긴 매개변수 목록을 가지고 있습니다. 자원 할당 목록은 가능한 많은 사용 사례를 포괄할 수 있도록 특히 확장되어 있습니다.

### **Links**

- **community.vmware.vmware_guest**
https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_module.html

### **Code**

다음은 `shim-ansible-test`라는 이름의 가상 머신을 생성하기 위한 코드입니다. 이 가상 머신은 다음과 같은 자원을 할당받습니다.:

<aside>
⚠️ **요구사항:
  -** 1 CPU
  - 1GB RAM
  - 10GB of thin-provisioned storage in the datastore named NETAPP_CA 
  - network card named DPG-CA-192.168.50.x  of type vmxnet3

</aside>

> create_vm.yml
> 

```yaml
---
- name: Create a VMware virtual machine
  hosts: localhost
  gather_facts: no
  vars:
    vcenter_hostname: "vc02.lab.iroo.int"
    vcenter_username: "administrator@vsphere.local"
    vcenter_password: "Ir00info1!"
    datacenter_name: "LvDC"
    cluster_name: "LvCL"
    datastore_name: "NETAPP_CA"
    network_name: "DPG-CA-192.168.50.x"
    vm_name: "shim-test-from-ansible"
    vm_cpu: 2
    vm_memory: 2024
    vm_disk_size: 20
    vm_guest_os: "centos64Guest"

  tasks:
    - name: Create a new VM
      community.vmware.vmware_guest:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: no
        cluster: "{{ cluster_name }}"
        datacenter: "{{ datacenter_name }}"
        datastore: "{{ datastore_name }}"
        folder: /CA
        name: "{{ vm_name }}"
        state: poweredon
        guest_id: "{{ vm_guest_os }}"
        networks:
          - name: "{{ network_name }}"
            device_type: vmxnet3
        hardware:
          num_cpu_cores_per_socket: 1
          num_cpus: "{{ vm_cpu }}"
          memory_mb: "{{ vm_memory }}"
        disk:
          - size_gb: "{{ vm_disk_size }}"
            type: thin
        wait_for_ip_address: yes
      delegate_to: localhost
      register: deploy_vm

    - name: Display VM details
      debug:
        msg: "Virtual machine {{ vm_name }} has been created successfully."

```

이 코드는 Ansible Playbook을 사용하여 다음과 같은 자원을 가진 가상 머신을 생성합니다:

- **가상 머신 이름**: `shim-ansible-test`
- **CPU**: 1개
- **메모리**: 1GB (1024MB)
- **디스크 크기**: 10GB, Thin 프로비저닝
- **운영 체제**: "centos64Guest" (다른 게스트 OS 유형에 맞게 조정 가능)

매개변수는 `vars` 섹션에서 정의하며, `community.vmware.vmware_guest` 모듈을 사용하여 VMware vSphere에 가상 머신을 생성합니다. 필요한 정보를 적절히 설정한 후, 이 Playbook을 실행하면 `shim-ansible-test` 가상 머신이 생성됩니다.

# [**04. 템플릿으로부터 VM 배포하기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 가상 머신 템플릿의 배포를 Ansible Playbook과 `vmware_guest` 모듈을 사용하여 자동화할 수 있습니다. VMware 가상 머신 템플릿은 미리 생성된 이미지로, 이 이미지를 마스터 이미지로 사용하여 VMware 인프라에서 더 많은 가상 머신을 생성할 수 있습니다. 템플릿 이미지는 설치된 기본 운영 체제와 가장 많이 사용되는 기업 소프트웨어가 포함된 미리 준비된 마스터 이미지를 사용하여 게스트 가상 머신의 프로비저닝 과정을 단순화합니다. 특히 Microsoft Windows 운영 체제에서 유용하며, VMware가 내부적으로 활성화 및 시리얼 번호 키를 처리합니다.

템플릿에서 가상 머신을 배포하는 것은 VMware 인프라를 관리하는 사람에게 가장 반복적인 작업 중 하나입니다. 일반적으로 템플릿 복사 단계와 게스트 운영 체제를 사용자 정의하기 위한 매개변수 사양 단계로 나뉩니다. 이 작업은 종종 vSphere 클라이언트 또는 웹 사용자 인터페이스에서 양식을 작성해야 하므로 일부 인간의 상호작용이 필요합니다. 이 작업은 인간 의존성이 있기 때문에 오류가 발생할 수 있습니다.

## **Ansible Module vmware_guest**

- **community.vmware.vmware_guest**

다음은 템플릿 `shim-linux-rocky9.2-template`에서 가상 머신 `shim-vm-from-template`을 사용자 정의 없이 배포하는 방법을 보여주는 Ansible Playbook입니다 (그림 3-2 참조). 이 Playbook에는 VMware 인프라의 공통 변수를 위한 `vars.yml` 파일과 데이터스토어에 가상 머신 폴더를 생성하는 작업, 그리고 템플릿에서 가상 머신을 배포하는 작업이 포함되어 있습니다.

### **Links**

- **community.vmware.vmware_guest** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 `shim-linux-rocky9.2-template` 템플릿으로부터 커스터마이징 없이 `shim-vm-from-template`이라는 가상 머신을 배포하는 방법을 보여드리겠습니다. 이 Ansible Playbook에는 VMware 인프라를 위한 공통 변수를 포함한 `vars.yml` 파일과, 데이터스토어에 가상 머신 폴더를 생성하는 작업 두 가지와 템플릿에서 가상 머신을 배포하는 작업 하나가 포함되어 있습니다.

> **vm_deploy_template.yml**
> 

```yaml
---
- name: deploy vm from template demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: create VM folder
      vcenter_folder:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter_name: "{{ vcenter_datacenter }}"
        folder_name: "{{ vcenter_destination_folder }}"
        folder_type: vm
        state: present
    - name: deploy VM from template
      vmware_guest:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        cluster: "{{ vcenter_cluster }}"
        name: "{{ vm_name }}"
        folder: "{{ vcenter_destination_folder }}"
        template: "{{ vm_template }}"
      delegate_to: localhost
      register: deploy_vm
    
    - name: Display VM details
      debug:
        msg: "Virtual machine {{ vm_name }} has been created successfully."

```

> vars.yml
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
vcenter_destination_folder: "CA"
vm_state: "poweroff"
vm_template: "shim-linux-rocky9.2-template"
```

# [**05. VM 전원 켜기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible Playbook과 `vmware_guest_powerstate` 모듈을 사용하여 VMware 가상 머신 게스트의 시작을 자동화할 수 있습니다. 일부 조직에서는 off-peak 및 on-peak 시간 관리를 위해, 백업 목적, 야간 유지보수, 또는 환경적인 이유로 가상 머신을 종료합니다. 이유가 무엇이든, Ansible은 몇 줄의 코드로 가상 머신 라이프사이클을 자동화할 수 있습니다. VMware 인프라 관리자에게 있어 가상 머신의 전원 상태 전환 관리 작업은 가장 단순한 활동 중 하나입니다. 전통적으로 가상 머신의 전원 상태를 수동으로 변경하려면 vSphere 클라이언트나 웹 사용자 인터페이스에 접근해야 합니다. 이 절차는 잘못된 가상 머신을 켜거나 끄면 오류가 발생할 수 있습니다. 예를 들어, Ansible Playbook과 `vmware_guest_powerstate` 모듈을 사용하여 가상 머신 게스트 `shim-vm-from-template`의 전원 꺼짐 상태에서 켜짐 상태로 전환하는 작업을 자동화해 보겠습니다.

## **Ansible Module vmware_guest_powerstate**

- **community.vmware.vmware_guest_powerstate**

Ansible 모듈 `vmware_guest_powerstate`를 사용하여 VMware 인프라 내의 모든 가상 머신의 전원 상태를 관리할 수 있습니다. `vmware_guest_powerstate` 모듈의 전체 이름은 `community.vmware.vmware_guest_powerstate`로, 이는 VMware와 상호 작용하는 모듈 모음의 일부이며 커뮤니티에서 지원된다는 의미입니다. 이 모듈은 vCenter의 가상 머신 전원 상태를 관리합니다.

### **Parameters**

다음은 `vmware_guest_powerstate` 모듈의 매개변수에 대한 설명입니다:

- `hostname` (string) / `port` (integer) / `username` (string) / `password` (string) / `datacenter` (string) / `validate_certs` (boolean): 연결 세부 정보
    - `hostname`: vCenter 서버의 호스트 이름 또는 IP 주소
    - `port`: 연결할 포트 번호
    - `username`: vCenter에 연결할 사용자 이름
    - `password`: vCenter에 연결할 비밀번호
    - `datacenter`: 가상 머신이 위치한 데이터 센터 이름
    - `validate_certs`: SSL 인증서를 검증할지 여부 (`true` 또는 `false`)
- `state` (string): 가상 머신의 목표 전원 상태
    - 가능한 값: `present` / `powered-off` / `powered-on` / `reboot-guest` / `restarted` / `shutdown-guest` / `suspended`
- `force` (boolean): 강제 실행 여부
    - 가능한 값: `no` / `yes`
- `answer` (string): 작업을 완료하는 동안 발생할 수 있는 질문에 대한 답변 목록

다음 매개변수는 `vmware_guest_powerstate` 모듈을 사용하여 VMware vSphere 가상 머신을 시작하는 데 유용합니다. 먼저, `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`와 같은 자기 설명적인 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다. 연결이 성공적으로 설정되면, 원하는 전원 상태(이 경우, `powered-on`)를 지정할 수 있습니다. `force` 매개변수를 사용하여 전원 상태 변경을 강제할 수도 있습니다(기본값: 비활성화). 작업 완료를 기다리는 동안 발생할 수 있는 질문에 대한 답변을 지정할 수도 있습니다. 일반적인 사용 예로는 잠겨 있는 CD-ROM을 변경하거나 VM이 복사되었는지 이동되었는지에 대한 질문에 답변하는 것이 있습니다.

### **Links**

- **community.vmware.vmware_guest_powerstate** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_powerstate_module.html

### **Code**

다음은 가상 머신 `shim-vm-from-template`을 전원 꺼짐 상태에서 전원 켜짐 상태로 전환하는 Ansible Playbook 예제입니다. 이 Ansible Playbook은 VMware 인프라의 공통 변수를 포함하는 `vars.yml` 파일과 지정된 이름 `shim-vm-from-template`의 가상 머신을 시작하는 하나의 작업으로 구성되어 있습니다. Ansible은 Python 라이브러리를 통해 VMware API와 상호 작용하여 이 작업을 수행하고 가상 머신의 성공적인 시작을 확인합니다.

> **vm_start.yml**
> 

```yaml
---
- name: [**VM 전원 켜기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: [**VM 전원 켜기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)
      vmware_guest_powerstate:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        name: "{{ vm_name }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        state: powered-on
```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
```

# [**06. VM 중지 또는 전원끄기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible Playbook과 `vmware_guest_powerstate` 모듈을 사용하여 VMware 가상 머신 게스트를 자동으로 종료할 수 있습니다. 만약 기업에서 백업 목적, 야간 유지보수 또는 환경적인 이유로 피크 타임이 아닐 때 가상 머신을 종료하는 데 익숙하다면, Ansible 자동화 플랫폼을 활용할 수 있습니다. 몇 줄의 코드로 쉽게 가상 머신 수명 주기를 자동화할 수 있으며, 이는 VMware 인프라 관리자에게 지루한 활동 중 하나입니다. 아마도 수동 방법에 익숙할 것입니다: 가상 머신을 종료하기 위해 vSphere 클라이언트나 웹 사용자 인터페이스에 액세스해야 하는 방법입니다. 올바른 가상 머신을 종료하는 데 매우 신중해야 합니다. 게다가, 가상 머신은 운영 체제가 ACPI를 지원하지 않거나, 게스트 운영 체제에 문제가 있거나, 단순히 첫 시도에서 작동하지 않는 경우 강제로 종료해야 할 때가 있습니다. 이제 Ansible Playbook과 `vmware_guest_powerstate` 모듈을 사용하여 전원 상태를 `Powered On`에서 `Powered Off`로 변경하기 위해, 우아한 게스트 종료와 강제 전원 끄기를 자동화해 보겠습니다.

## **Ansible Module vmware_guest_powerstate**

- **community.vmware.vmware_guest_powerstate**

VMware 인프라의 모든 가상 머신의 전원 상태를 Ansible 모듈 `vmware_guest_powerstate`를 사용하여 관리할 수 있습니다. `vmware_guest_powerstate` 모듈의 전체 이름은 `community.vmware.vmware_guest_powerstate`이며, 이는 VMware와 상호 작용하는 모듈 모음의 일부로 커뮤니티에서 지원된다는 의미입니다. 이 모듈은 vCenter 내의 가상 머신의 전원 상태를 관리합니다.

### **Parameters**

다음은 `vmware_guest_powerstate` 모듈의 매개변수에 대한 설명입니다:

- `hostname` (string) / `port` (integer) / `username` (string) / `password` (string) / `datacenter` (string) / `validate_certs` (boolean): 연결 세부 정보
    - `hostname`: vCenter 서버의 호스트 이름 또는 IP 주소
    - `port`: 연결할 포트 번호
    - `username`: vCenter에 연결할 사용자 이름
    - `password`: vCenter에 연결할 비밀번호
    - `datacenter`: 가상 머신이 위치한 데이터 센터 이름
    - `validate_certs`: SSL 인증서를 검증할지 여부 (`true` 또는 `false`)
- `state` (string): 가상 머신의 목표 전원 상태
    - 가능한 값: `present` / `powered-off` / `powered-on` / `reboot-guest` / `restarted` / `shutdown-guest` / `suspended`
- `force` (boolean): 강제 실행 여부
    - 가능한 값: `no` / `yes`
- `answer` (string): 작업을 완료하는 동안 발생할 수 있는 질문에 대한 답변 목록

다음 매개변수는 `vmware_guest_powerstate` 모듈을 사용하여 VMware vSphere 가상 머신을 시작하는 데 유용합니다. 먼저, 많은 설명이 필요 없는 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다: `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`. 연결이 성공적으로 설정되면 원하는 전원 상태를 지정할 수 있습니다. 이 경우, `shutdown-guest`는 게스트 운영 체제에 정상적으로 종료를 요청하는 것이며, `powered-off`는 가상 머신 게스트의 전원을 끄는 것입니다. 또한, `force` 매개변수를 사용하여 전원 상태를 강제로 변경할 수 있습니다(기본값: 비활성화).

### **Links**

- **community.vmware.vmware_guest_powerstate** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_powerstate_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 `shim-vm-from-template`이라는 가상 머신의 전원 상태를 `Powered On`에서 `Powered Off`로 변경하는 방법입니다. 먼저 `shutdown-guest` 작업을 시도하여 게스트 운영 체제에 정상적으로 종료를 요청한 다음 `powered-off` 작업을 통해 가상 머신 게스트를 강제로 종료해 보겠습니다. 이 Ansible Playbook은 VMware 인프라에 대한 공통 변수를 포함하는 `vars.yml` 파일을 포함하고 있으며, 지정된 이름 `shim-vm-from-template`을 가진 가상 머신의 전원을 관리하는 하나의 작업이 있습니다. 내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호 작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다. 게스트 종료 작업을 위한 시간 초과는 120초(2분)로 설정됩니다. `vmware_guest_powerstate` 모듈의 기본값은 종료 신호를 보낸 후 즉시(값 0) 반환합니다.

> **vm_stop.yml**
> 

```yaml
---
- name: VM 전원끄기
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: guest shutdown
      vmware_guest_powerstate:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        state: shutdown-guest
        state_change_timeout: 120
      register: shutdown
      ignore_errors: true
    - name: poweroff
      vmware_guest_powerstate:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        state: powered-off
      when: shutdown.failed

```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
```

# [**07. VM 스냅샷 생성**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 가상 머신의 스냅샷을 자동으로 생성하는 과정을 Ansible Playbook과 `vmware_guest_snapshot` 모듈을 사용하여 자동화할 수 있습니다. VMware 가상 머신 스냅샷은 가상 머신의 특정 상태를 시간 지점에서 저장하는 편리한 방법입니다. 가상화는 실행 중에도 스냅샷을 찍을 수 있게 해줍니다. Veeam Backup 과 Replication과 같은 일부 기업 백업 솔루션은 VMware 스냅샷 기능에 의존합니다. 전통적인 방법으로 가상 머신의 스냅샷을 수동으로 찍으려면 vSphere 클라이언트나 웹 사용자 인터페이스에 접근해야 합니다. 하나의 VMware 스냅샷을 실행하기 위해서는 여러 차례 사용자 인터페이스와 상호작용이 필요합니다. Ansible 관점에서 `vmware_guest_snapshot` 모듈은 이 예제에서 `shim-vm-from-template`이라는 이름으로 가상 머신을 식별하며, 원하는 스냅샷 이름을 정의할 수 있습니다. 예를 들어, `Ansible Managed Snapshot`이라는 이름을 지정하여 쉽게 찾을 수 있습니다. 스냅샷이 쌓이기 시작하면 이름과 설명 기능이 정말 유용할 것입니다! 날짜와 시간 표기를 선호하는 경우, `ansible_date_time` Ansible fact 변수를 사용하세요. 특히, 날짜와 시간의 글로벌 표준인 ISO 8601 표기를 위해, Ansible Playbook에서 `ansible_date_time.iso8601`을 지정하면 `2024-08-02T00:45:55+0000`와 같은 값을 얻을 수 있습니다. 

## **Ansible Module vmware_guest_snapshot**

- **community.vmware.vmware_guest_snapshot**

VMware 스냅샷을 관리하려면 Ansible 모듈 `vmware_guest_snapshot`을 사용할 수 있습니다. 이 모듈의 전체 이름은 `community.vmware.vmware_guest_snapshot`이며, 이는 VMware와 상호 작용하는 모듈 모음의 일부로 커뮤니티에서 지원된다는 의미입니다. 이 모듈은 vCenter 내의 가상 머신 스냅샷을 관리합니다.

### **Parameters**

다음은 `vmware_guest_snapshot` 모듈을 사용하여 VMware 스냅샷을 관리할 때 유용한 매개변수입니다:

- **hostname** (*string*) : VMware vSphere 또는 vCenter의 호스트 이름을 지정합니다.
- **port** (*integer*) : VMware vSphere 또는 vCenter의 포트 번호를 지정합니다.
- **username** (*string*) : VMware vSphere 또는 vCenter에 로그인할 사용자 이름을 지정합니다.
- **password** (*string*) : VMware vSphere 또는 vCenter에 로그인할 비밀번호를 지정합니다.
- **datacenter** (*string*) : 스냅샷을 관리할 데이터 센터의 이름을 지정합니다.
- **validate_certs** (*boolean*) : SSL 인증서 유효성 검사를 수행할지 여부를 설정합니다. (기본값: `false`)
- **state** (*string*) : 스냅샷의 상태를 정의합니다:
    - `present` : 스냅샷을 생성합니다.
    - `absent` : 스냅샷을 삭제합니다.
    - `revert` : 스냅샷으로 복원합니다.
    - `remove_all` : 모든 스냅샷을 제거합니다.
- **remove_children** (*boolean*) : 스냅샷을 삭제할 때 자식 스냅샷도 함께 삭제할지 여부를 설정합니다. (기본값: `no`)
- **snapshot_name** (*string*) : 작업할 가상 머신의 스냅샷 이름을 지정합니다.
- **description** (*string*) : 스냅샷에 대한 설명을 제공하여 나중에 쉽게 식별할 수 있도록 합니다.
- **memory_dump** (*boolean*) : 메모리 덤프를 포함할지 여부를 설정합니다. 메모리 스냅샷은 시간과 자원을 소모하므로 필요에 따라 사용합니다. (기본값: `no`)

다음 매개변수는 `vmware_guest_snapshot` 모듈을 사용하여 VMware 가상 머신 스냅샷을 찍을 때 유용합니다. 우선, `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`와 같은 여러 자명한 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다. 연결이 성공적으로 설정되면, 원하는 스냅샷 상태를 지정할 수 있습니다. 이 경우, `present`를 설정하여 스냅샷을 찍을 수 있습니다. 같은 Ansible 모듈을 사용하여 스냅샷을 복원하거나 삭제할 수도 있습니다. 스냅샷을 삭제하려는 경우, `remove_children` 매개변수를 사용하여 모든 의존 스냅샷을 함께 제거할 수도 있습니다. 스냅샷의 이름과 설명을 `snapshot_name` 및 `description` 매개변수를 사용하여 설정하는 것은 좋은 습관입니다. 고급 방법으로는 가상 머신의 메모리 덤프를 생성하는 것이 있습니다. 메모리 스냅샷은 생성하는 데 시간이 더 걸리고 자원을 소모하므로 기본적으로는 비활성화되어 있지만, `memory_dump` 매개변수를 사용하여 활성화할 수 있습니다.

### **Links**

- **community.vmware.vmware_guest_snapshot** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_snapshot_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 `shim-vm-from-template` 이라는 가상 머신의 스냅샷을 `Ansible Managed Snapshot`이라는 이름으로 찍는 방법입니다. 스냅샷에 이름과 설명을 설정하여 VMware vCenter에서 쉽게 찾을 수 있도록 하세요. Ansible Playbook에는 VMware 인프라를 위한 공통 변수를 포함한 `vars.yml` 파일이 포함되어 있으며, 지정된 이름 `shim-vm-from-template`의 가상 머신에 대해 스냅샷을 찍는 하나의 작업이 포함되어 있습니다. Ansible은 VMware API와 상호 작용하여 작업을 실행하고 가상 머신의 스냅샷 생성 성공 여부를 확인합니다.

![Screenshot 2024-07-29 at 2.02.04 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/18aedfb3-b723-47a6-bd00-20f686739deb/Screenshot_2024-07-29_at_2.02.04_PM.png)

> **vm_snapshot_create.yml**
> 

```yaml
---
- name: VM 스냅샷 생성
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: VM 스냅샷 생성
      community.vmware.vmware_guest_snapshot:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        state: present
        snapshot_name: "Ansible Managed Snapshot"
        folder: "{{ vm_folder }}"
        description: "This snapshot is created by Ansible Playbook"
      delegate_to: localhost
```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
vm_folder: "CA"
```

# [**08. VM 스냅샷 삭제**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 가상 머신의 스냅샷을 찍고 제거하는 과정을 자동화하려면 Ansible Playbook과 `vmware_guest_snapshot` 모듈을 사용할 수 있습니다. VMware 가상 머신 스냅샷은 가상 머신의 특정 상태를 저장하는 강력한 방법이지만, 스냅샷이 쌓이기 시작하면 관리가 어려워집니다. 스냅샷의 수가 많을수록 저장 공간의 사용량이 증가하므로, 좋은 스냅샷 관리가 항상 좋은 최선의 실천입니다.

전통적으로 스냅샷을 수동으로 찍으려면 vSphere 클라이언트나 웹 사용자 인터페이스에 접근해야 하며, 하나의 VMware 스냅샷을 삭제하기 위해서는 여러 번의 상호작용이 필요합니다. Ansible 관점에서 보면, `vmware_guest_snapshot` 모듈은 이 예제에서 `shim-vm-from-template` 이라는 이름의 가상 머신을 식별하며, 원하는 스냅샷 이름, 예를 들어 "Ansible Managed Snapshot"을 검색할 수도 있습니다.

## **Ansible Module vmware_guest_snapshot**

- **community.vmware.vmware_guest_snapshot**

VMware 스냅샷은 Ansible 모듈 `vmware_guest_snapshot`을 사용하여 관리할 수 있습니다. 이 모듈의 전체 이름은 `community.vmware.vmware_guest_snapshot`으로, 이는 VMware와 상호작용하는 모듈 컬렉션의 일부이며, 커뮤니티에서 지원됩니다. 이 모듈은 vCenter에서 가상 머신 스냅샷을 관리합니다.

### **Parameters**

다음은 `vmware_guest_snapshot` 모듈을 사용하여 VMware 스냅샷을 관리할 때 유용한 매개변수들입니다:

- **hostname** (*string*): VMware vSphere 또는 vCenter 서버의 호스트 이름.
- **port** (*integer*): VMware 서버의 포트 번호.
- **username** (*string*): VMware 서버에 로그인할 사용자 이름.
- **password** (*string*): VMware 서버에 로그인할 비밀번호.
- **datacenter** (*string*): 가상 머신이 위치한 데이터 센터의 이름.
- **validate_certs** (*boolean*): SSL 인증서 검증 여부. (예: `yes` 또는 `no`)
- **state** (*string*): 스냅샷의 상태를 지정합니다. 사용 가능한 값은 `present` (스냅샷을 생성), `absent` (스냅샷을 제거), `revert` (스냅샷으로 복원), `remove_all` (모든 스냅샷 제거)입니다.
- **remove_children** (*boolean)*: 스냅샷 삭제 시 종속된 스냅샷을 함께 제거할지 여부. (예: `yes` 또는 `no`)
- **snapshot_name** (*string*): 작업할 가상 머신의 스냅샷 이름.
- **description** (*string*): 스냅샷에 대한 설명.

다음은 `vmware_guest_snapshot` 모듈을 사용하여 VMware 가상 머신 스냅샷을 생성하는 데 유용한 매개변수들입니다. 먼저, VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다. 이를 위해 다음과 같은 설명이 명확한 매개변수를 사용합니다: `hostname`, `username`, `password`, `datacenter`, `validate_certs`. 연결이 성공적으로 설정되면, 원하는 스냅샷 상태를 지정할 수 있습니다. 이 경우, 스냅샷을 삭제하려면 `absent` 상태를 설정합니다. 같은 Ansible 모듈을 사용하여 스냅샷을 관리할 수 있습니다. 스냅샷을 제거하려면, `remove_children` 매개변수를 사용하여 모든 종속 스냅샷도 함께 제거할 수 있습니다. `snapshot_name` 매개변수에 제거할 스냅샷의 정확한 이름을 지정해야 합니다.

### **Links**

- community.vmware.vmware_guest_snapshot https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_snapshot_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 가상 머신 `shim-vm-from-template` 의 스냅샷 `Ansible Managed Snapshot`을 삭제하는 방법을 보여드리겠습니다 (실행 전 상태는 그림 3-9, 실행 후 상태는 그림 3-10 참조). Ansible Playbook은 VMware 인프라를 위한 공통 변수를 포함한 `vars.yml` 파일을 포함하고 있으며, 지정된 이름 `shim-vm-from-template`을 가진 가상 머신의 스냅샷을 삭제하는 작업을 하나 포함하고 있습니다. Ansible은 내부적으로 Python 라이브러리를 통해 VMware API와 상호 작용하여 작업을 실행하고 가상 머신의 상태를 성공적으로 확인합니다.

> **vm_snapshot_remove.yml**
> 

```yaml
---
- name: VM 스냅샷 삭제
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: VM 스냅샷 삭제
      vmware_guest_snapshot:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        folder: "{{ vm_folder }}"
        snapshot_name: "Ansible Managed Snapshot"
        state: absent
```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
vm_folder: "CA"
```

# [**09. VM에 하드디스크 추가**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

다음은 Ansible Playbook과 `vmware_guest_disk` 모듈을 사용하여 VMware 가상 머신 게스트에 새 하드 디스크를 추가하는 방법입니다. 이는 가상 머신에 추가 저장소를 추가할 때 유용하며, VMware 인프라 관리자에게는 지루한 작업 중 하나입니다. 수동으로 하드 디스크를 추가하려면 몇 가지 양식을 작성하고 vSphere 클라이언트나 웹 사용자 인터페이스에 접근해야 합니다. 하드 드라이브를 올바른 가상 머신에 연결하는 것이 문제의 원인이 될 수 있으므로 매우 주의해야 합니다. 일부 운영 체제는 저장소 핫플러그를 지원하지만 대부분의 운영 체제는 저장소 구성을 변경하기 전에 가상 머신을 종료해야 합니다. 각 가상 하드 드라이브는 가상 저장소 컨트롤러에 연결되어야 합니다. VMware는 가장 많이 사용되는 SCSI 컨트롤러 유형(BusLogic Parallel, LSI Logic Parallel, LSI Logic SAS, VMware Paravirtual SCSI)과 AHCI, SATA, 최신 릴리스 및 NVM Express (NVMe) 컨트롤러를 지원합니다. 최신 릴리스에서 실행 중인 VMware 인프라 버전의 지원되는 최대 가상 저장소 컨트롤러 수(최대 네 개의 SCSI 컨트롤러와 네 개의 SATA 컨트롤러)를 확인하십시오. Ansible Playbook과 `vmware_guest_disk` 모듈을 사용하여 `shim-vm-from-template`이라는 VMware 가상 머신 게스트에 10GB 하드 디스크를 추가하는 방법을 살펴보겠습니다. 이 작업은 가상 하드 드라이브만 추가하며, 파티션을 나누고 파일 시스템을 포맷하는 작업은 운영 체제에서 수행해야 합니다. 이 작업은 운영 체제에 따라 다릅니다: Linux는 CLI와 GUI 도구인 `fdisk`, `parted`, `gparted`, `qtparted`, `KDE Partition Manager` 및 `GNOME Disks Utility`를 사용하며, macOS는 `Disk Utility`를 사용하고, Windows는 `Disk Management`를 사용합니다.

## **Ansible Module vmware_guest_disk**

- **community.vmware.vmware_guest_disk**

VMware 가상 하드 드라이브를 관리하려면 Ansible 모듈 `vmware_guest_disk`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vmware_guest_disk`이며, 이는 VMware와 상호 작용하는 모듈 모음의 일부로 커뮤니티 지원을 받는다는 것을 의미합니다. 이 모듈은 주어진 vCenter 인프라에서 가상 머신과 관련된 디스크를 관리합니다.

### **Parameters**

다음은 Ansible 모듈 `vmware_guest_disk`를 사용하여 VMware 가상 하드 드라이브를 관리할 때 유용한 매개변수입니다:

- **hostname** string: VMware vSphere 또는 vCenter 서버의 호스트 이름
- **port** integer: 서버 포트 번호
- **username** string: VMware에 로그인할 사용자 이름
- **password** string: VMware에 로그인할 비밀번호
- **datacenter** string: 가상 머신이 속한 데이터 센터 이름
- **validate_certs** boolean: SSL 인증서 검증 여부 (예: `yes` 또는 `no`)
- **datacenter** string: 가상 머신이 속한 데이터 센터의 이름
- **scsi_controller/unit_number/scsi_type** string: SCSI 컨트롤러 관련 세부 사항
- **scsi_controller**: SCSI 컨트롤러 유형 (예: BusLogic Parallel, LSI Logic Parallel, LSI Logic SAS, VMware Paravirtual SCSI 등)
- **unit_number**: SCSI 장치의 유닛 번호
- **scsi_type**: SCSI 장치의 유형
- **size/size_kb/size_mb/size_gb/size_tb** string: 디스크 스토리지 크기
- **size**: 디스크 크기 (예: "10G" 또는 "10GB")
- **size_kb**: 디스크 크기 (킬로바이트 단위)
- **size_mb**: 디스크 크기 (메가바이트 단위)
- **size_gb**: 디스크 크기 (기가바이트 단위)
- **size_tb**: 디스크 크기 (테라바이트 단위)
- **disk_mode** string — 디스크 모드 설정
- **persistent**: 지속적인 디스크 모드
- **independent_persistent**: 독립적인 지속적인 디스크 모드
- **independent_nonpersistent**: 독립적인 비지속적인 디스크 모드

다음은 Ansible 모듈 `vmware_guest_disk`를 사용하여 VMware 가상 머신에 디스크를 추가할 때 유용한 매개변수입니다:

1. **연결 설정**:
    - **hostname**: VMware vSphere 또는 vCenter 서버의 호스트 이름
    - **username**: VMware에 로그인할 사용자 이름
    - **password**: VMware에 로그인할 비밀번호
    - **datacenter**: 가상 머신이 속한 데이터 센터 이름
    - **validate_certs**: SSL 인증서 검증 여부 (예: `yes` 또는 `no`)
2. **디스크 구성**:
    - **datacenter**: 자원 할당을 위해 가상 머신이 속한 데이터 센터의 이름을 지정합니다. 필수 매개변수입니다.
    - **unit_number**: SCSI 컨트롤러의 유닛 번호를 지정합니다. 필수 매개변수입니다.
    - **scsi_controller**: 디스크가 연결될 SCSI 컨트롤러의 유형을 지정합니다.
    - **scsi_type**: SCSI 장치의 유형을 지정합니다.
    
    SCSI 표준에 따르면 유효한 SCSI 컨트롤러 번호는 0에서 29까지이며, 유닛 번호는 0에서 15까지입니다. 성능 분석을 통해 이러한 매개변수를 적절하게 조정하는 것이 중요할 수 있습니다.
    
3. **디스크 크기**:
    - **size/size_kb/size_mb/size_gb/size_tb**: 디스크 크기를 지정하는 다양한 매개변수입니다. 필요에 따라 크기 단위를 선택할 수 있습니다 (kb, MB, GB, TB 등).
4. **디스크 모드**:
    - **disk_mode**: 디스크 모드를 설정하는 매개변수로, 기본값은 `persistent`입니다. 다른 옵션으로는 `independent_persistent` 및 `independent_nonpersistent`이 있습니다.

이러한 매개변수를 통해 VMware 가상 머신에 새 디스크를 추가하거나 기존 디스크를 관리할 수 있습니다.

### **Links**

- **community.vmware.vmware_guest_disk** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_disk_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 `shim-vm-from-template`이라는 가상 머신에 10GB 디스크를 추가하는 방법입니다. 이 디스크는 SCSI 컨트롤러 번호 1과 유닛 번호 1에 추가됩니다. Ansible Playbook에는 VMware 인프라를 위한 공통 변수를 포함한 `vars.yml` 파일이 있으며, 지정된 이름 `shim-vm-from-template`을 가진 가상 머신에 디스크를 추가하는 작업이 포함되어 있습니다. Ansible은 Python 라이브러리를 통해 VMware API와 상호 작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

![Screenshot 2024-07-29 at 2.35.15 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/902419df-7e63-4a89-abb1-2543ba5a5a36/Screenshot_2024-07-29_at_2.35.15_PM.png)

> **vm_add_disk.yml**
> 

```yaml
---
- name: VM에 하드디스크 추가
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: VM에 하드디스크 추가
      vmware_guest_disk:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        name: "{{ vm_name }}"
        disk:
          - size_gb: "{{ vm_disk_gb }}"
            type: "{{ vm_disk_type }}"
            datastore: "{{ vm_disk_datastore }}"
            state: present
            scsi_controller: "{{ vm_disk_scsi_controller }}"
            unit_number: "{{ vm_disk_scsi_unit }}"
            scsi_type: "{{ vm_disk_scsi_type }}"
            disk_mode: "{{ vm_disk_mode }}"

```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
vm_folder: "CA"
vm_disk_gb: 10
vm_disk_type: "thin"
vm_disk_datastore: "NETAPP_CA"
vm_disk_scsi_controller: 1
vm_disk_scsi_unit: 1
vm_disk_scsi_type: 'paravirtual'
vm_disk_mode: 'persistent'
```

# [**10. VM의 가상디스크 확장**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

다음은 Ansible Playbook과 `vmware_guest_disk` 모듈을 사용하여 VMware 가상 머신의 하드 디스크를 확장하는 자동화 방법입니다. 이는 가상 머신의 저장소를 관리하는 데 유용하며, VMware 인프라 관리자가 수행해야 하는 지루한 작업 중 하나입니다.

수동으로 작업하는 방법은 vSphere 클라이언트나 웹 사용자 인터페이스에 접근하여 폼을 이용해 작업해야 하며, 이러한 수동 작업은 인간 의존적이어서 오류가 발생할 가능성이 높습니다. 예를 들어, 잘못된 가상 머신에 공간을 확장하면 어떻게 될까요? VMware는 가상 디스크를 축소할 수 없으므로, 유일한 옵션은 백업에서 가상 머신을 복구하는 것입니다 (백업이 있는 경우).

## **Ansible Module vmware_guest_disk**

- **community.vmware.vmware_guest_disk**

VMware 가상 하드 드라이브를 관리하려면 Ansible 모듈 `vmware_guest_disk`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vmware_guest_disk`이며, 이는 VMware와 상호 작용하는 모듈 컬렉션의 일부이며 커뮤니티에서 지원됩니다. 이 모듈은 특정 vCenter 인프라 내의 가상 머신과 관련된 디스크를 관리합니다.

### **Parameters**

다음은 VMware 가상 머신에 디스크를 추가하거나 관리할 때 유용한 `vmware_guest_disk` 모듈의 매개변수입니다:

1. **연결 설정**:
    - **hostname (***string***)**: VMware vSphere 또는 vCenter의 호스트 이름.
    - **port (***integer***)**: 연결에 사용할 포트 번호.
    - **username (***string***)**: VMware vSphere 또는 vCenter에 로그인할 사용자 이름.
    - **password (***string***)**: VMware vSphere 또는 vCenter에 로그인할 비밀번호.
    - **datacenter (***string***)**: 가상 머신이 속한 데이터센터의 이름.
    - **validate_certs (***boolean***)**: 인증서 유효성 검사를 수행할지 여부 (기본값은 `yes`, 인증서 검사를 수행하지 않으려면 `no`로 설정).
2. **데이터센터 이름**:
    - **datacenter (***string***)**: 디스크를 추가할 가상 머신이 속한 데이터센터의 이름을 지정합니다.
3. **SCSI 컨트롤러 세부 사항**:
    - **scsi_controller (***string***)**: SCSI 컨트롤러의 번호.
    - **unit_number (***integer***)**: SCSI 컨트롤러 내에서 디스크의 장치 번호.
    - **scsi_type (***string***)**: SCSI 컨트롤러의 유형 (예: BusLogic Parallel, LSI Logic Parallel, LSI Logic SAS 등).
4. **디스크 크기**:
    - **size (***string***)**: 디스크의 크기를 지정할 때 사용할 수 있는 다양한 단위:
        - **size_kb (***string***)**: 킬로바이트 단위로 디스크 크기 지정.
        - **size_mb (***string***)**: 메가바이트 단위로 디스크 크기 지정.
        - **size_gb (***string***)**: 기가바이트 단위로 디스크 크기 지정.
        - **size_tb (***string***)**: 테라바이트 단위로 디스크 크기 지정.
5. **디스크 모드**:
    - **disk_mode (***string***)**: 디스크의 모드를 설정합니다. 가능한 옵션은:
        - **persistent**: 디스크의 모든 변경 사항이 유지되는 기본 모드.
        - **independent_persistent**: 디스크의 변경 사항이 독립적으로 유지됩니다.
        - **independent_nonpersistent**: 디스크의 변경 사항이 독립적으로 유지되지 않고, 재부팅 시 모든 변경 사항이 사라집니다.

이 매개변수들을 적절히 설정하면 VMware 가상 머신의 디스크를 효율적으로 관리할 수 있습니다.

### **Links**

- **community.vmware.vmware_guest_disk** https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_disk_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 가상 머신 이름이 `shim-vm-from-template`인 가상 머신에 연결된 추가 디스크의 크기를 확장하는 방법을 설명합니다. 디스크는 SCSI 컨트롤러 번호 1과 장치 번호 1에 연결되어 있습니다. 이 가상 하드 디스크는 10GB의 크기를 가지고 있으며, 이를 20GB로 확장하려고 합니다. Ansible Playbook에는 VMware 인프라를 위한 공통 변수들이 포함된 `vars.yml` 파일과 가상 머신 이름이 `shim-vm-from-template`인 가상 머신의 가상 하드 디스크 크기를 확장하는 하나의 작업이 포함되어 있습니다. Ansible은 내부적으로 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

![Screenshot 2024-07-29 at 2.48.19 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/3117ecab-bd79-4d5e-af95-e80479651af0/Screenshot_2024-07-29_at_2.48.19_PM.png)

> **vm_disk_expand.yml**
> 

```yaml
---
- name: [**VM의 가상디스크 확장**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: [**VM의 가상디스크 확장**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)
      vmware_guest_disk:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        name: "{{ vm_name }}"
        disk:
          - size_gb: "{{ vm_disk_gb }}"
            type: "{{ vm_disk_type }}"
            datastore: "{{ vm_disk_datastore }}"
            state: present
            scsi_controller: "{{ vm_disk_scsi_controller }}"
            unit_number: "{{ vm_disk_scsi_unit }}"
            scsi_type: "{{ vm_disk_scsi_type }}"
            disk_mode: "{{ vm_disk_mode }}"
    
    - name: Display VM details
      debug:
        msg: "A Disk of {{ vm_name }} has been expanded successfully."

```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
vm_folder: "CA"
vm_disk_gb: 20
vm_disk_type: "thin"
vm_disk_datastore: "NETAPP_CA"
vm_disk_scsi_controller: 1
vm_disk_scsi_unit: 1
vm_disk_scsi_type: 'paravirtual'
vm_disk_mode: 'persistent'
```

# [**11. 클러스터의 호스트 정보 수집하기**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 클러스터 내 VMware ESX/ESXi 호스트의 정보를 자동으로 수집할 수 있습니다. 이를 위해 Ansible Playbook과 `vmware_host_config_info` 모듈을 사용할 수 있습니다. Reporting은 모든 VMware 인프라 관리자들이 정기적으로 수행하는 좋은 관리 관행입니다. 보고를 통해 자원 계획, 할당, 및 최적화를 비즈니스 요구에 맞춰 조정할 수 있습니다. 아마도 여러분은 이 작업을 수동으로 수행하는 데 익숙할 것입니다. 이는 vSphere 클라이언트나 웹 사용자 인터페이스에 접근하여 각 클러스터와 VMware ESX/ESXi 호스트에 대해 다양한 양식을 탐색하는 방식입니다. 이러한 작업은 반복적이고 지루한 작업이므로, 자동화를 통해 오류를 방지하고 시간을 절약할 수 있습니다.

## **Ansible Module vmware_host_config_info**

- **community.vmware.vmware_host_config_info**

VMware ESXi 호스트에 대한 구성 및 실행 정보를 수집하려면 Ansible 모듈 `vmware_host_config_info`를 사용할 수 있습니다. 이 모듈의 전체 이름은 `community.vmware.vmware_host_config_info`이며, 이는 VMware와 상호 작용하는 모듈 모음의 일부로 커뮤니티 지원을 받는 모듈입니다. 이 모듈의 목적은 ESXi 호스트의 고급 구성 정보를 수집하는 것입니다.

### **Parameters**

다음은 ESXi 호스트에 대한 정보를 수집하기 위해 `vmware_host_config_info` 모듈에서 사용하는 유용한 매개변수입니다:

- **hostname** (*string*): VMware vCenter 또는 ESXi 호스트의 호스트네임
- **port** (*integer*): vCenter 또는 ESXi 호스트의 포트 번호
- **username** (*string*): 인증에 사용할 사용자 이름
- **password** (*string*): 인증에 사용할 비밀번호
- **datacenter** (*string*): 가상 머신이 속한 데이터센터의 이름
- **validate_certs** (*boolean*): 인증서 유효성 검사를 수행할지 여부 (예: `no`)
- **cluster_name** (*string*): ESXi 호스트가 속한 클러스터의 이름
- **esxi_hostname** (*string*): 정보를 수집할 ESXi 호스트의 호스트네임

이 매개변수들을 설정하여 VMware vSphere 또는 VMware vCenter에 연결하고, 클러스터 내의 모든 ESXi 호스트에 대한 정보를 수집할 수 있습니다. `esxi_hostname`을 지정하면 특정 ESXi 호스트에 대한 정보를 수집하고, 이를 생략하면 지정된 클러스터 내의 모든 ESXi 호스트에 대한 정보를 나열할 수 있습니다.

### **Links**

- community.vmware.vmware_host_config_info https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_cluster_info_module.html

### **Code**

다음은 현재 VMware `LvCL` 클러스터의 모든 ESXi 호스트에 대한 구성 정보를 수집하는 Ansible Playbook을 작성하는 방법입니다. 이 Ansible Playbook은 VMware 인프라에 대한 공통 변수를 포함하는 `vars.yml` 파일을 사용하며, 두 가지 작업이 포함되어 있습니다.

1. 첫 번째 작업은 VMware `LvCL` 클러스터에서 정보를 수집하여 `cluster_info` Ansible 변수에 결과를 저장합니다.
2. 두 번째 작업은 화면에 `cluster_info` Ansible 변수의 값을 출력합니다.

실제 시나리오에서는 `cluster_info` Ansible 변수의 상태를 기반으로 추가 작업을 수행할 수도 있습니다. Ansible은 Python 라이브러리를 통해 VMware API와 상호 작용하여 작업을 실행하고, 가상 머신의 성공적인 시작을 검증합니다.

여기서는 `vars.yml`과 `vmware_host_config_info` 모듈을 사용하여 ESXi 호스트 정보를 수집하고 출력하는 Playbook 예제를 제공합니다.

> **host_info_cluser.yml**
> 

```yaml
---
- name: host in cluster info demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: Gather info about all ESXi Host in the given Cluster
      community.vmware.vmware_host_config_info:
        hostname: '{{ vcenter_hostname }}'
        username: '{{ vcenter_username }}'
        password: '{{ vcenter_password }}'
        validate_certs: "{{ vcenter_validate_certs }}"
        cluster_name: "{{ cluster_name }}"
      register: cluster_info

    - name: print cluster info
      ansible.builtin.debug:
        var: cluster_info

```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
cluster_name: "LvCL"
```

# [12. VMware VM UUID 정보 얻기](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

다음은 Ansible Playbook과 `vmware_guest_info` 모듈을 사용하여 VMware 가상 머신의 UUID를 자동으로 수집하는 방법입니다. UUID(Universally Unique Identifier, 범용 고유 식별자)는 VMware 인프라에서 가상 머신을 유일하게 식별합니다. 가상 머신을 처음으로 전원 켤 때 생성됩니다. UUID는 일상적인 작업 수행뿐만 아니라 호스트 간 VMware 이동을 수행할 때 매우 유용합니다. 가상 머신 이름보다 나은 점은 가상 머신을 유일하게 식별할 수 있다는 것입니다. 단점은 128비트 정수로 구성되어 있어서 기억하기 쉽지 않다는 점입니다. 일반적으로 대시가 있는 16진수 값으로 표시됩니다.

## **Ansible Module vmware_guest_info**

- **community.vmware.vmware_guest_info**

다음은 VMware 가상 머신에 대한 정보를 수집하기 위해 Ansible 모듈 `vmware_guest_info`를 사용하는 방법입니다. 전체 이름은 `community.vmware.vmware_guest_info`로, VMware와 상호 작용하는 모듈 컬렉션의 일부이며, 커뮤니티에서 지원됩니다. 이 모듈의 목적은 단일 VM에 대한 정보를 수집하는 것입니다. `vmware_guest_info` 모듈은 이전에 사용되던 `community.vmware.vmware_guest_facts` 모듈의 대체 모듈로, `community.vmware.vmware_guest_facts` 모듈은 2021년 12월 1일 이후의 주요 릴리스에서 제거되었습니다. 

https://docs.ansible.com/ansible/2.10/collections/community/vmware/vmware_guest_facts_module.html

### **Parameters**

다음은 Ansible 모듈 `vmware_guest_info`를 사용하여 VMware 가상 머신에 대한 정보를 수집할 때 유용한 매개변수입니다:

- `hostname` (*string*): VMware vSphere 또는 VMware vCenter 서버의 호스트명
- `port` (*integer*): VMware vSphere 또는 VMware vCenter 서버의 포트 번호
- `username` (*string*): VMware vSphere 또는 VMware vCenter 서버에 로그인할 사용자 이름
- `password` (*string*): VMware vSphere 또는 VMware vCenter 서버에 로그인할 비밀번호
- `datacenter` (*string*): 가상 머신이 속한 데이터센터의 이름
- `validate_certs` (*boolean*): SSL 인증서 검증을 수행할지 여부
- `name` (*string*): 정보를 수집할 가상 머신의 이름

### **Links**

- community.vmware.vmware_guest_info https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_info_module.html

### **Code**

다음은 Ansible Playbook을 사용하여 특정 VMware 가상 머신(`shim-vm-from-template`)에 대한 정보를 수집하고 UUID를 선택하는 방법입니다. 이 Ansible Playbook은 VMware 인프라를 위한 공통 변수를 포함한 `vars.yml` 파일과 두 가지 작업을 포함합니다. 첫 번째 작업은 `shim-vm-from-template` VMware 가상 머신에서 정보를 수집하고 결과를 `detailed_vm_info` Ansible 변수에 저장합니다. 두 번째 작업은 `detailed_vm_info` Ansible 변수의 값을 화면에 출력합니다. 구체적으로, UUID 값은 `detailed_vm_info.instance.hw_product_uuid` 매개변수에 저장됩니다. Ansible은 VMware API와 Python 라이브러리를 통해 상호작용하여 작업을 실행하고 가상 머신의 시작을 확인합니다.

> **vm_uuid.yml**
> 

```yaml
---
- name: vm UUID demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: Get VM UUID
      vmware_guest_info:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
      register: detailed_vm_info

    - name: print VM UUID
      ansible.builtin.debug:
        var: detailed_vm_info.instance.hw_product_uuid

```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vm-from-template"
```

![Screenshot 2024-07-29 at 4.33.15 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/1f3a03de-7b37-4729-afa8-c1558f142ab2/Screenshot_2024-07-29_at_4.33.15_PM.png)

VMware vSphere 웹 사용자 인터페이스에서 VMware 가상 머신의 UUID를 확인할 수 있습니다. 이 정보는 VMware vSphere 웹 콘솔의 “호스트 및 클러스터(Hosts and Clusters)” 또는 “가상 머신 및 템플릿(VMs and Templates)”에서 찾을 수 있습니다. 목록 보기에서는 상태, 상태, 할당된 공간과 사용된 공간, 호스트 CPU, 메모리 등의 많은 정보를 확인할 수 있습니다. 목록에 UUID 열이 표시되지 않는 경우, 열의 회색 부분을 클릭하고 '열 표시/숨기기(Show/Hide Columns)'를 선택한 후 팝업 목록에서 UUID를 활성화하십시오. 

# [13. Ansible Dynamic Inventory](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 인프라에서 가상 머신 목록을 자동으로 나열하려면 `vmware_vm_inventory` Ansible 인벤토리 플러그인을 사용할 수 있습니다. 이 플러그인의 장점 중 하나는 동적 목록을 Ansible 인벤토리로 사용하여 실행할 수 있다는 점입니다. 인벤토리 플러그인은 지정된 데이터 소스에서 대상 노드의 목록을 즉시 생성하여 Ansible의 기능을 확장할 수 있게 해줍니다. 데이터 소스에는 VMware 인프라에 대한 연결 매개변수가 포함되며, 출력에는 모든 가상 머신의 목록이 포함됩니다. 이 작업을 수동으로 수행할 방법은 없으며, VMware 가상 머신의 Ansible 인벤토리를 수동으로 생성해야 합니다. Ansible 인벤토리의 수동 생성은 본질적으로 오류가 발생하기 쉬운데, 간단한 오타조차도 실패나 잘못된 대상 호스트와 같은 실행에 큰 영향을 미칠 수 있습니다.

## **Ansible vmware_vm_inventory**

- **community.vmware.vmware_vm_inventory**

Ansible 인벤토리 플러그인은 VMware API를 통해 VMware 인프라를 쿼리하고 Ansible에 사용할 수 있는 가상 머신 목록을 반환합니다. 그 목적은 VMware 환경에서 가상 머신을 인벤토리 호스트로 가져오는 것입니다. 이렇게 하면 모든 가상 머신에 대해 Ansible 자동화를 실행할 수 있습니다. 예를 들어, 모든 가상 머신에 대해 자동화를 수행할 수 있습니다.

인벤토리 YAML 구성 파일의 이름은 반드시 `vmware.yml`, `vmware.yaml`, `vmware_vm_inventory.yml`, 또는 `vmware_vm_inventory.yaml`로 끝나야 합니다. 전체 이름은 `community.vmware.vmware_vm_inventory`이며, 이는 VMware와 상호작용하는 모듈 모음의 일부이며 커뮤니티에서 지원되는 모듈입니다.

- **Python requirements**

`community.vmware` 컬렉션과 마찬가지로, 이 플러그인은 Ansible 컨트롤러에 `pyVmomi` Python 라이브러리가 설치되어 있어야 합니다. 태그 기능과 같은 고급 매개변수를 사용하려면 VMware vSphere Automation SDK for Python 라이브러리도 설치해야 합니다.

### **Links**

- community.vmware.vmware_vm_inventory https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_vm_inventory_inventory.html

### **Code**

다음 예제에서는 이 책에서 이전에 생성한 `shim-vm-from-template` 테스트 머신을 포함하여 사용 가능한 모든 가상 머신을 나열하는 방법을 설명합니다.

첫 번째 단계는 구성 파일에서 `vmware_vm_inventory` Ansible 인벤토리 플러그인을 활성화하는 것입니다. 현재 경로에 있는 `ansible.cfg` 파일이나 시스템 전체에서 `/etc/ansible/ansible.cfg` 파일을 통해 이를 활성화할 수 있습니다. 인벤토리 섹션의 `enable_plugins` 키 안에 `vmware_vm_inventory` 플러그인 이름을 추가하기만 하면 됩니다.

> **ansible.cfg**
> 

```yaml
[inventory]
enable_plugins = vmware_vm_inventory
```

두 번째 단계는 VMware 인프라 연결 매개변수로 데이터 소스를 생성하는 것입니다. 다음은 `vmware.example.com` VMware vSphere에 연결하여 모든 가상 머신을 나열하는 간단한 YAML 데이터 소스입니다. 이 데이터 소스는 주어진 사용자 이름과 비밀번호를 사용하여 연결하며, SSL 인증서 검증을 비활성화합니다 (자체 서명된 인증서의 경우). 또한 VMware 가상 머신 결과의 그룹 매핑을 활성화하며, VMware 가상 머신에 연결된 태그를 비활성화합니다 (vSphere Automation SDK Python 라이브러리가 필요합니다).

> **inventory.vmware.yml**
> 

```yaml
---
plugin: community.vmware.vmware_vm_inventory
strict: False
hostname: vc02.lab.iroo.int
username: administrator@vsphere.local
password: Ir00info1!
validate_certs: False
with_tags: False

```

기본적으로 출력되는 뷰는 VMware 가상 머신과 관련된 모든 VMware 속성을 표시합니다. YAML 데이터 소스에서 `properties` 매개변수를 지정하면 필요한 속성만 표시할 수 있습니다. 예를 들어, `name`, `config.cpuHotAddEnabled`, `config.cpuHotRemoveEnabled`, `config.instanceUuid`, `config.hardware.numCPU`, `config.template`, `config.name`, `config.uuid`, `guest.hostName`, `guest.ipAddress`, `guest.guestId`, `guest.guestState`, `runtime.maxMemoryUsage`, `customValue`, `summary.runtime.powerState`, `config.guestId`와 같은 속성들을 지정할 수 있습니다.

```yaml
properties:
  - 'runtime.powerState'
  - 'config.name'
```

`filters` 매개변수는 특정 상태의 가상 머신만 검색할 수 있게 해주는 유용한 매개변수입니다. 다음은 `filters` 매개변수를 사용하여 전원이 켜진 상태의 가상 머신만 검색하는 예제입니다:

```yaml
filters:
  - runtime.powerState == "poweredOn"
```

다음은 특정 운영 체제 클래스가 있는 가상 시스템만 검색하는 필터 매개 변수의 예입니다:

```yaml
filters:
  - config.guestId == "rhel7_64Guest"
```

ansible-inventory 도구는 인벤토리 데이터 소스 inventory.vmware.yml을 입력으로 사용하여 JSON 목록 보기를 생성할 수 있습니다.

```yaml
ansible-inventory -i inventory.vmware.yml --list
```

성공적인 실행 출력에는 myVMware 가상 시스템에 대한 다음과 같은 출력이 포함됩니다:

# [**14. 가상머신이 실행 중인 호스트 정보**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible 플레이북과 vmware_guest_info 모듈을 사용하여 VMware 가상 머신의 실행 중인 호스트 정보를 자동으로 수집할 수 있습니다. vmware_guest_info 모듈에 대한 자세한 내용은 "[12. VMware 가상 머신 UUID 얻기](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)" 섹션을 참조하십시오. VMware 가상 머신의 현재 실행 중인 호스트에 접근하는 것은 인프라의 현재 부하 분포에 대한 정확한 보고서를 작성하고, VMware 호스트 자원 간의 작업 부하를 더 잘 분배하며, 일상적인 운영 작업과 호스트 간의 VMware 모션을 수행하는 데 유용합니다.

### Link

**community.vmware.vmware_guest_info module**

[community.vmware.vmware_guest_info module – Gather info about a single VM — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_info_module.html)

### Code

Ansible 플레이북을 사용하여 myvm VMware 가상 머신에 대한 정보를 수집하고 실행 중인 호스트를 선택하는 방법을 보여드리겠습니다. Ansible 플레이북에는 VMware 인프라를 위한 공통 변수를 포함한 vars.yml 파일과 두 개의 작업이 포함되어 있습니다. 첫 번째 작업은 myvm VMware 가상 머신에서 정보를 가져와서 detailed_vm_info Ansible 변수에 결과를 저장합니다. 두 번째 작업은 detailed_vm_info Ansible 변수의 값을 화면에 출력합니다. 구체적으로, 실행 중인 호스트 값은 detailed_vm_info.instance.hw_esxi_host 반환 값에 저장됩니다. 내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **vm_running_host.yml**
> 

```yaml
---
- name: vm running host demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: Get VM info
      **vmware_guest_info**:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
      register: detailed_vm_info
    - name: print VM Running Host
      ansible.builtin.debug:
        var: detailed_vm_info.instance.hw_esxi_host
```

`vars.yml` 파일은 여러 Ansible Playbook 파일에서 공유될 수 있는 모든 VMware 인프라 연결 매개변수를 저장합니다.

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int "
vcenter_datacenter: "LvDC"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-vcsa"
```

Ansible 인벤토리는 Ansible 컨트롤러에서 Ansible 자동화를 실행하고 있기 때문에 localhost만 포함됩니다.

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=3 changed=0
- 반환 값:
    
    ```yaml
    TASK [print VM Running Host] *************************************************************************************************************************
    ok: [localhost] => {
        "detailed_vm_info.instance.hw_esxi_host": "vl04.lab.iroo.int"
    }
    ```
    

이 코드는 반복 실행해도 동일한 결과를 산출합니다.

VMware vSphere 웹 사용자 인터페이스의 "**Summary**" 페이지에 있는 "**host**" 필드에서 VMware 가상 머신의 실행 중인 호스트를 수집한 결과를 확인할 수 있습니다(그림 3-16 참조).

![***Figure 3-16*** Getting a VMware virtual machine running host via the VMware vSphere web UI](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/3cc5d8ed-41bb-43ef-a52a-2bae2e7f9f83/Screenshot_2024-08-26_at_3.33.00_PM.png)

***Figure 3-16*** Getting a VMware virtual machine running host via the VMware vSphere web UI

# [**15. Datastore 상태 정보 확인**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible Playbook과 `vmware_datastore_info` 모듈을 사용하여 VMware vSphere 데이터스토어의 상태 수집을 자동화할 수 있습니다(그림 3-17 참조). VMware vSphere의 데이터스토어는 가상 머신과 VMFS 파일 시스템을 사용하는 VMware 리소스를 위한 저장소 자원입니다. VMware 인프라 관리자들은 스토리지가 Helthy하고 성능 좋은 인프라의 중요한 역할을 한다는 것을 알고 있습니다. VMware 데이터스토어의 현재 용량, 할당된 공간, 남은 공간, 유지보수 모드 정보에 대한 정확한 보고서는 VMware 리소스 간 워크로드를 더 잘 분배하는 데 필수적이며, 일상적인 작업뿐만 아니라 VMware 스토리지 모션을 수행하는 데도 유용합니다.

## **Ansible Module vmware_datastore_info**

- **community.vmware.vmware_datastore_info**

[community.vmware.vmware_datastore module – Configure Datastores — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_datastore_module.html)

VMware 데이터스토어에 대한 정보를 수집하려면 Ansible 모듈 `vmware_datastore_info`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vmware_datastore_info`로, 이는 VMware와 상호 작용하는 모듈 컬렉션의 일부이며 커뮤니티 지원을 받는 모듈입니다. 이 모듈의 목적은 특정 VMware vCenter에서 사용할 수 있는 데이터스토어에 대한 정보를 수집하는 것입니다.

### **Parameters**

다음 매개변수는 `vmware_datastore_info` 모듈을 사용하여 VMware vSphere 데이터스토어 상태를 얻는 데 유용합니다. 먼저, 다음과 같은 직관적인 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와 연결을 설정해야 합니다: `hostname`(호스트명), `port`(포트), `username`(사용자 이름), `password`(비밀번호), `datacenter`(데이터센터), `validate_certs`(인증서 검증 여부). 연결이 성공적으로 설정되면, `name`(데이터스토어 이름)을 지정하여 데이터스토어에 대한 모든 정보를 얻을 수 있습니다.

### **Links**

[**community.vmware.vmware_datastore_info](https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_datastore_info_module.html), https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_datastore_info_module.html**

### **Code**

특정 VMware vSphere 데이터스토어에 대한 정보를 수집하는 방법을 Ansible Playbook을 사용하여 보여드리겠습니다 (그림 3-17 참조). 이 Ansible Playbook에는 VMware 인프라를 위한 일부 공통 변수를 포함하는 `vars.yml` 파일이 있으며, 두 가지 작업이 포함되어 있습니다. 첫 번째 작업은 VMware vSphere 데이터스토어로부터 정보를 획득하고 결과를 `datastore_info` Ansible 변수에 저장합니다. 두 번째 작업은 화면에 `datastore_info` Ansible 변수의 값을 출력합니다. 내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **datastore_info.yml**
> 

```yaml
---
- name: datastore info demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: datastore info
      vmware_datastore_info:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter_name: "{{ vcenter_datacenter }}"
        name: "{{ vcenter_datastore }}"
      register: datastore_info
    - name: print datastore info
      ansible.builtin.debug:
        var: datastore_info
```

`vars.yml` 파일은 여러 Ansible Playbook 파일에서 공유될 수 있는 모든 VMware 인프라 연결 매개변수를 저장합니다.

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int "
vcenter_datacenter: "LvDC"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vcenter_datastore: "NETAPP_CA"
```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=3 changed=0
- 반환 값:
    
    ```yaml
    ok: [localhost] => {
        "msg": {
            "changed": false,
            "datastores": [
                {
                    "accessible": true,
                    "capacity": 3133608140800,
                    "datastore_cluster": "N/A",
                    "freeSpace": 1781704425472,
                    "maintenanceMode": "normal",
                    "multipleHostAccess": true,
                    "name": "**NETAPP_CA**",
                    "provisioned": 5310993661952,
                    "type": "NFS",
                    "uncommitted": 3959089946624,
                    "url": "ds:///vmfs/volumes/6b9a781d-8825837f/"
                }
            ],
            "failed": false
        }
    }
    ```
    

VMware vSphere 데이터스토어 상태와 정보를 수집한 결과를 VMware vSphere 웹 사용자 인터페이스에서 확인할 수 있습니다(그림 3-17 참조). 이 정보는 VMware vSphere 웹 콘솔의 "**Storage**" 영역에서 찾을 수 있습니다.

![***Figure 3-17*** Getting VMware datastore status in the VMware vSphere web UI](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/8efa8e10-4590-4763-8740-ce79ff2e0662/Screenshot_2024-08-26_at_3.50.14_PM.png)

***Figure 3-17*** Getting VMware datastore status in the VMware vSphere web UI

# [**16. File을 Datastore에 업로드**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware vSphere 데이터스토어에 파일을 업로드하는 작업을 Ansible Playbook과 `vsphere_copy` 모듈을 사용하여 자동화할 수 있습니다 (실행 전은 그림 3-18 참조, 실행 후는 그림 3-19 참조). VMware 데이터스토어는 VMware 호스트 간에 가상 머신과 VMware 리소스가 공유되는 VMware 저장소 영역입니다. VMware 인프라 관리자는 새로운 VMware 가상 머신을 생성하기 전에 ISO 이미지 파일을 업로드합니다.

## **Ansible Module vsphere_copy**

- **community.vmware.vsphere_copy**

VMware 데이터스토어에 대한 정보를 수집하려면 Ansible 모듈 `vsphere_copy`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vsphere_copy`로, 이는 VMware와 상호 작용하는 모듈 컬렉션의 일부이며 커뮤니티 지원을 받는 모듈입니다. 이 모듈의 목적은 파일을 VMware vSphere 데이터스토어에 복사하는 것입니다.

### **Parameters**

- **hostname**: 문자열 - VMware vSphere 또는 VMware vCenter의 호스트 이름
- **port**: 정수 - 연결에 사용할 포트 번호
- **username**: 문자열 - 로그인할 때 사용할 사용자 이름
- **password**: 문자열 - 로그인할 때 사용할 비밀번호
- **datacenter**: 문자열 - 데이터스토어가 위치한 데이터센터의 이름
- **validate_certs**: 불리언 - SSL 인증서 검증 여부
- **datastore**: 문자열 - 데이터스토어의 이름
- **src**: 문자열 - 원본 파일 이름
- **path**: 문자열 - 대상 파일 이름

다음 매개변수는 `vsphere_copy` 모듈을 사용하여 파일을 VMware vSphere 데이터스토어에 복사하는 데 유용합니다. 먼저, `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`와 같은 직관적인 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와 연결을 설정해야 합니다. 연결이 성공적으로 설정되면, Ansible 컨트롤러 파일 시스템의 원본 파일(`src`), 대상 VMware 데이터스토어(`datastore`), 및 대상 경로(`path` 또는 데이터스토어 파일 이름)를 지정할 수 있습니다.

### **Links**

[**community.vmware.vsphere_copy](https://docs.ansible.com/ansible/latest/collections/community/vmware/vsphere_copy_module.html), https://docs.ansible.com/ansible/latest/collections/community/vmware/vsphere_copy_module.html**

### **Code**

`VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso`VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso ISO 이미지를 VMware vSphere 데이터스토어에 업로드하는 방법을 Ansible Playbook을 사용하여 보여드리겠습니다. 원본 경로와 대상 경로는 변수 `mysrc`와 `mydest`로 지정되며, 이를 Ansible Playbook에서 사용자 정의하거나 명령줄을 통해 추가 변수로 사용할 수 있습니다. Ansible Playbook에는 VMware 인프라를 위한 일부 공통 변수를 포함하는 `vars.yml` 파일이 있으며, 하나의 작업이 포함되어 있습니다. 내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **datastore_info.yml**
> 

```yaml
---
- name: datastore copy demo
  hosts: localhost
  gather_facts: false
  vars:
    mysrc: "iso/VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso"
    mydest: "VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso"
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: copy file to datastore
      vsphere_copy:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        datastore: "{{ vcenter_datastore }}"
        src: "{{ mysrc }}"
        path: "{{ mydest }}"
```

> **vars.yml**
> 

```yaml
---
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vcenter_datastore: "NETAPP_CA"

```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=2 changed=1
- 반환 값:
    
    ```yaml
    TASK [copy file to datastore] ********************************************************************************************************************
    changed: [localhost]
    ```
    

실행이 실패한 출력은 실패 이유를 명시합니다. 다음 예제에서는 원본 파일 `iso/VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso`가 해당 디렉토리에 존재하지 않기 때문에 실패한 것입니다.

- 대상 호스트: localhost
- 명령 결과: failed=1
- 반환 값:

```yaml
TASK [copy file to datastore]
fatal: [localhost]: FAILED! => {"changed": false, "msg": "Failed to open src file [Errno 2] No such file or directory: 'iso/VMware-VMvisor-Installer-8.0U3-24022510.x86_64.iso'"}
```

파일을 VMware vSphere 데이터스토어에 업로드한 결과를 VMware vSphere 웹 사용자 인터페이스에서 확인할 수 있습니다. 이 정보는 VMware vSphere 웹 콘솔의 "**Storage**" 영역에서 찾을 수 있습니다. "**Files**" 영역을 통해 데이터스토어 경로를 탐색할 수 있습니다.

![Screenshot 2024-08-26 at 4.03.56 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/d6cbd9d0-7c69-46d0-a8e1-22da186e6548/Screenshot_2024-08-26_at_4.03.56_PM.png)

***Figure 3-19*** After uploading a file to the VMware datastore

# [**17. VMware Tools 상태 정보 확인**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 가상 머신 게스트 도구의 상태를 수집하는 작업을 Ansible Playbook과 `vmware_guest_tools_info` 모듈을 사용하여 자동화할 수 있습니다 (그림 3-20 참조). VMware 게스트 도구는 게스트 운영 체제의 성능 향상과 VMware 가상 머신과의 원활한 사용자 상호작용을 위한 서비스와 모듈의 집합입니다. VMware 가상 머신에서 VMware 게스트 도구의 현재 상태(실행 중, 실행 안 됨, 최신, 설치되지 않음)에 대한 정확한 보고서는 VMware 인프라 전반에 걸쳐 워크로드 분배의 성능을 향상시키는 데 중요합니다.

## **Ansible Module vmware_guest_tools_info**

- **community.vmware.vmware_guest_tools_info**

VMware 게스트 도구의 상태에 대한 정보를 수집하려면 Ansible 모듈 `vmware_guest_tools_info`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vmware_guest_tools_info`로, 이는 VMware와 상호작용하는 모듈 컬렉션의 일부이며 커뮤니티 지원을 받는 모듈입니다. 이 모듈의 목적은 VMware 가상 머신에 설치된 VMware 게스트 도구에 대한 정보를 수집하는 것입니다.

### **Parameters**

- **hostname**: 문자열 - VMware vSphere 또는 VMware vCenter의 호스트 이름
- **port**: 정수 - 연결에 사용할 포트 번호
- **username**: 문자열 - 로그인할 때 사용할 사용자 이름
- **password**: 문자열 - 로그인할 때 사용할 비밀번호
- **datacenter**: 문자열 - 데이터스토어가 위치한 데이터센터의 이름
- **validate_certs**: 불리언 - SSL 인증서 검증 여부
- **name**: 문자열 - 가상 머신의 이름

다음 매개변수는 `vmware_guest_tools_info` 모듈을 사용하여 VMware 게스트 도구 상태를 얻는 데 유용합니다. 먼저, `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`와 같은 직관적인 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와 연결을 설정해야 합니다. 연결이 성공적으로 설정되면, VMware 가상 머신 이름을 지정하여 해당 가상 머신에 설치된 VMware 게스트 도구에 대한 모든 정보를 얻을 수 있습니다.

### **Links**

[**community.vmware.vmware_guest_tools_info](https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_tools_info_module.html), https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_tools_info_module.html**

### **Code**

특정 `myvm` VMware 가상 머신에 대한 정보를 수집하고 실행 중인 호스트를 선택하는 방법을 Ansible Playbook을 사용하여 보여드리겠습니다 (그림 3-20 참조). 이 Ansible Playbook에는 VMware 인프라를 위한 일부 공통 변수를 포함하는 `vars.yml` 파일이 있으며, 두 가지 작업이 포함되어 있습니다.

1. 첫 번째 작업은 `myvm` VMware 가상 머신으로부터 정보를 획득하고 결과를 `vmtools_info` Ansible 변수에 저장합니다.
2. 두 번째 작업은 `debug` Ansible 모듈을 사용하여 `vmtools_info` Ansible 변수의 값을 화면에 출력합니다.

내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **vm_guest_tools_info.yml**
> 

```yaml
---
- name: vmware guest tools info demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: guest tools info
      vmware_guest:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        name: "{{ vm_name }}"
      register: vmtools_info
    - name: print guest tools info
      ansible.builtin.debug:
        var: vmtools_info
```

> **vars.yml**
> 

```yaml
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-AD-50.253-tanzukr.com"
```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=2 changed=1
- 반환 값:
    
    ```yaml
    TASK [print guest tools info] ********************************************************************************************************************
    ok: [localhost] => {
        "vmtools_info": {
            "changed": false,
            "deprecations": [
                {
                    "collection_name": "community.vmware",
                    "msg": "The API providing vm_tools_install_status has been deprecated by VMware; use vm_tools_running_status / vm_tools_version_status instead",
                    "version": "5.0.0"
                }
            ],
            "failed": false,
            "vmtools_info": {
                "vm_guest_fullname": "Microsoft Windows Server 2019 (64-bit)",
                "vm_guest_hostname": "AD.tanzukr.com",
                "vm_guest_id": "windows2019srv_64Guest",
                "vm_hw_version": "vmx-17",
                "vm_ipaddress": "192.168.50.253",
                "vm_moid": null,
                "vm_name": "shim-AD-50.253-tanzukr.com",
                "vm_tools_install_status": "toolsOk",
                "vm_tools_install_type": "guestToolsTypeMSI",
                "vm_tools_last_install_count": 3,
                "vm_tools_running_status": "guestToolsRunning",
                "vm_tools_upgrade_policy": "manual",
                "vm_tools_version": 12384,
                "vm_tools_version_status": "guestToolsCurrent",
                "vm_use_instance_uuid": false,
                "vm_uuid": null
            }
        }
    }
    ```
    

이 경우, VMware 가상 머신 `myvm`의 VMware 게스트 도구 상태는 다음과 같습니다:

- VMware 게스트 도구 설치됨 (`vm_tools_version_status`: "toolsOk")
- VMware 게스트 도구 실행 중 (`vm_tools_running_status`: "guestToolsRunning")
- VMware 게스트 도구 유형 OpenVM (`vm_tools_install_type`: "guestToolsTypeOpenVMTools")
- VMware 게스트 도구 업그레이드 정책 수동 (`vm_tools_upgrade_policy`: "manual")

VMware 게스트 도구가 없는 가상 머신의 성공적인 실행 출력은 다음과 같습니다:

- 대상 호스트: localhost
- 명령 결과: ok=3 changed=0
- 반환 값:
    
    ```yaml
    TASK [guest tools info]
    ok: [localhost]
    TASK [print guest tools info]
    ok: [localhost] => {
        "vmtools_info": {
            "changed": false,
            "failed": false,
            "vmtools_info": {
                "vm_name": "myvm",
                "vm_tools_install_status": "toolsNotInstalled",
                "vm_tools_install_type": "guestToolsTypeUnknown",
                "vm_tools_last_install_count": 0,
                "vm_tools_running_status": "**guestToolsNotRunning**",
                "vm_tools_upgrade_policy": "manual",
                "vm_tools_version": 0,
                "vm_tools_version_status": "guestToolsNotInstalled",
            }
        }
    }
    
    ```
    

이 경우, VMware 가상 머신 `myvm`의 VMware 게스트 도구 상태는 다음과 같습니다:

- VMware 게스트 도구 설치되지 않음 (`vm_tools_version_status`: "guestToolsNotInstalled")
- VMware 게스트 도구 실행되지 않음 (`vm_tools_running_status`: "guestToolsNotRunning")
- VMware 게스트 도구 업그레이드 정책 수동 (`vm_tools_upgrade_policy`: "manual")

특정 가상 머신의 VMware 게스트 도구 상태를 수집한 결과는 VMware vSphere 웹 사용자 인터페이스의 "**Summary**" 페이지에 있는 "VMware Tools" 필드에서 확인할 수 있습니다. 그림 3-20을 참조하십시오.

![***Figure 3-20*** VMware guest tools status in VMware vSphere web UI](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/8a4418e7-e0b3-4f28-acb2-84f8a9609129/Screenshot_2024-08-26_at_5.58.05_PM.png)

***Figure 3-20*** VMware guest tools status in VMware vSphere web UI

# [**18. VMware Tool 업그레이드**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware 가상 머신 게스트 도구의 업그레이드를 Ansible Playbook과 `vmware_guest_tools_upgrade` 모듈을 사용하여 자동화할 수 있습니다 (실행 전은 그림 3-21 참조, 실행 후는 그림 3-22 참조). 최신 VMware 게스트 도구를 유지하는 것은 VMware 가상 머신에서 최상의 성능을 얻기 위한 좋은 실천입니다. 업그레이드 절차는 VMware 게스트 도구와 Open VM Tools(open-vm-tools, Linux 게스트 운영 체제를 위한 오픈 소스 구현)를 지원합니다.

## **Ansible Module vmware_guest_tools_upgrade**

- **community.vmware.vmware_guest_tools_upgrade**

VMware 데이터스토어에 대한 정보를 수집하려면 Ansible 모듈 `vmware_guest_tools_upgrade`를 사용할 수 있습니다. 전체 이름은 `community.vmware.vmware_guest_tools_upgrade`로, 이는 VMware와 상호작용하는 모듈 컬렉션의 일부이며 커뮤니티 지원을 받는 모듈입니다. 이 모듈의 목적은 VMware 가상 머신에 설치된 VMware 게스트 도구를 원활하게 업그레이드하는 것입니다.

### **Parameters**

- **hostname**: 문자열 - VMware vSphere 또는 VMware vCenter의 호스트 이름
- **port**: 정수 - 연결에 사용할 포트 번호
- **username**: 문자열 - 로그인할 때 사용할 사용자 이름
- **password**: 문자열 - 로그인할 때 사용할 비밀번호
- **datacenter**: 문자열 - 데이터스토어가 위치한 데이터센터의 이름
- **validate_certs**: 불리언 - SSL 인증서 검증 여부
- **name**: 문자열 - 가상 머신의 이름

다음 매개변수는 `vmware_guest_tools_upgrade` 모듈을 사용하여 VMware 게스트 도구를 업그레이드하는 데 유용합니다. 먼저, `hostname`, `port`, `username`, `password`, `datacenter`, `validate_certs`와 같은 직관적인 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와 연결을 설정해야 합니다. 연결이 성공적으로 설정되면, VMware 가상 머신 이름을 지정하여 해당 가상 머신에 설치된 VMware 게스트 도구에 대한 모든 정보를 얻을 수 있습니다.

### **Links**

[**community.vmware.vmware_guest_tools_upgrade](https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_tools_upgrade_module.html), https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_tools_upgrade_module.html**

### **Code**

`myvm` VMware 가상 머신의 게스트 도구를 업그레이드하는 방법을 보여드리겠습니다. 이 Ansible Playbook에는 VMware 인프라를 위한 공통 변수를 포함하는 `vars.yml` 파일이 있으며, 다섯 가지 작업이 포함되어 있습니다.

1. 첫 번째 작업은 `myvm` VMware 가상 머신이 전원이 켜져 있는지 확인합니다.
2. 두 번째 작업은 `myvm` VMware 가상 머신의 UUID를 가져와 `detailed_vm_info` Ansible 변수에 결과를 저장합니다.
3. 세 번째 작업은 `detailed_vm_info.instance.hw_product_uuid` Ansible 변수를 사용하여 VMware 게스트 도구 업그레이드를 실행합니다 (참고: “VMware 가상 머신 UUID 가져오기” 섹션).
4. 네 번째 작업은 업데이트된 VMware 게스트 도구 정보를 얻어 `vmtools_info` Ansible 변수에 저장합니다.
5. 마지막 작업은 `vmtools_info` Ansible 변수의 값을 화면에 출력하기 위해 `debug` Ansible 모듈을 사용합니다.

내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **vm_guest_tools_upgrade.yml**
> 

```yaml
---
- name: vmware guest tools upgrade demo
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: VM powered-on
      vmware_guest_powerstate:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        state: powered-on
    - name: VM get UUID
      vmware_guest_info:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        datacenter: "{{ vcenter_datacenter }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
      register: detailed_vm_info
    - name: vmware guest tools upgrade
      vmware_guest_tools_upgrade:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        uuid: "{{ detailed_vm_info.instance.hw_product_uuid }}"
    - name: guest tools info
      vmware_guest_tools_info:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        datacenter: "{{ vcenter_datacenter }}"
        name: "{{ vm_name }}"
      register: vmtools_info
    - name: print guest tools info
      ansible.builtin.debug:
        var: vmtools_info
```

> **vars.yml**
> 

```yaml
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-AD-50.253-tanzukr.com"
```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=6 changed=1
- 반환 값:
    
    ```yaml
    ok: [localhost] => {
        "vmtools_info": {
            "changed": false,
            "deprecations": [
                {
                    "collection_name": "community.vmware",
                    "msg": "The API providing vm_tools_install_status has been deprecated by VMware; use vm_tools_running_status / vm_tools_version_status instead",
                    "version": "5.0.0"
                }
            ],
            "failed": false,
            "vmtools_info": {
                "vm_guest_fullname": "Microsoft Windows Server 2019 (64-bit)",
                "vm_guest_hostname": "AD.tanzukr.com",
                "vm_guest_id": "windows2019srv_64Guest",
                "vm_hw_version": "vmx-17",
                "vm_ipaddress": "192.168.50.253",
                "vm_moid": null,
                "vm_name": "**shim-AD-50.253-tanzukr.com**",
                "vm_tools_install_status": "toolsOld",
                "vm_tools_install_type": "guestToolsTypeMSI",
                "vm_tools_last_install_count": 1,
                "vm_tools_running_status": "guestToolsRunning",
                "vm_tools_upgrade_policy": "manual",
                "vm_tools_version": 12325,
                "vm_tools_version_status": "guestToolsSupportedOld",
                "vm_use_instance_uuid": false,
                "vm_uuid": null
            }
        }
    }
    ```
    

실행 후, VMware 가상 머신 `myvm`의 VMware 게스트 도구 상태는 다음과 같습니다:

- VMware 게스트 도구 설치됨 (`vm_tools_version_status`: "toolsOk")
- VMware 게스트 도구 실행 중 (`vm_tools_running_status`: "guestToolsRunning")
- VMware 게스트 도구 유형 OpenVM (`vm_tools_install_type`: "guestToolsTypeOpenVMTools")

VMware 게스트 도구가 성공적으로 설치되어야만 업그레이드를 성공적으로 수행할 수 있습니다. 실패한 실행 출력에는 치명적인 오류 메시지가 포함됩니다:

- 대상 호스트: localhost
- 명령 결과: ok=3 failed=1
- 반환 값:
    
    ```yaml
    TASK [VM powered-on]
    ok: [localhost]
    TASK [VM get UUID]
    ok: [localhost]
    TASK [vmware guest tools upgrade]
    fatal: [localhost]: FAILED! => {"changed": false, "msg": "VMware tools is either not running or not installed"}
    ```
    

특정 가상 머신의 VMware 가상 머신 게스트 도구 업그레이드 결과를 VMware vSphere 웹 사용자 인터페이스의 "**Summary**" 페이지에 있는 "VMware Tools" 필드에서 확인할 수 있습니다. 그림 3-21 및 3-22를 참조하십시오.

![***Figure 3-21*** Before the VMware guest tools upgrade in the VMware vSphere web UI](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/167cf9ba-1b51-4b6f-9bca-15c7eae4d9fc/Screenshot_2024-08-26_at_5.45.40_PM.png)

***Figure 3-21*** Before the VMware guest tools upgrade in the VMware vSphere web UI

![***Figure 3-22*** After the VMware guest tools upgrade in the VMware vSphere web UI](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/25777fab-2d06-4cd9-8124-321e3b746028/Screenshot_2024-08-26_at_5.47.23_PM.png)

***Figure 3-22*** After the VMware guest tools upgrade in the VMware vSphere web UI

# [**19. vMotion을 이용한 Live Migration**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

VMware vMotion, Ansible Playbook, 그리고 vmware_vmotion 모듈을 사용하여 VMware 가상 머신 게스트의 라이브 마이그레이션을 자동화할 수 있습니다(실행 전의 상태는 그림 3-23에서, 실행 후의 상태는 그림 3-24에서 확인할 수 있습니다). Storage vMotion 기능도 가능합니다. Ansible은 vmware_vmotion 모듈을 통해 VMware vMotion의 이점을 활용하여 VMware 인프라에서 더 많은 자동화 시나리오를 가능하게 합니다. 예를 들어, 호스트의 전원을 끄기 위해 자원을 체계적으로 이동시키거나 더 나은 자원 할당을 제공할 수 있습니다.

## **Ansible vmware_vmotion Module**

**• community.vmware.vmware_vmotion**

Ansible 모듈 vmware_vmotion은 VMware vMotion 기술을 사용하여 VMware 인프라 내의 VMware 가상 머신을 이동하는 데 사용됩니다. 이 모듈의 전체 이름은 community.vmware.vmware_vmotion이며, 이는 VMware와 상호작용하는 모듈 컬렉션의 일부이며 커뮤니티에서 지원된다는 것을 의미합니다. 이 모듈의 목적은 vMotion을 사용하여 가상 머신을 이동하는 것입니다.

**Parameters**

- hostname 문자열/port 정수/username 문자열/password 문자열/datacenter 문자열/validate_certs  부울: 연결 세부 정보
- destination_host문자열: 대상 VMware 호스트
- destination_datastore 문자열: 대상 VMware 데이터스토어
- destination_datacenter 문자열: 대상 VMware 데이터센터
- destination_cluster 문자열: 대상 VMware 클러스터
- destination_resourcepool 문자열: 대상 VMware 리소스 풀
- destination_datastore_cluster 문자열: 대상 VMware 데이터스토어 클러스터(스토리지 팟)

다음 매개변수들은 vmware_vmotion 모듈을 사용하여 VMware 가상 머신을 vMotion을 통해 라이브 마이그레이션하는 데 유용합니다. 먼저, hostname, port, username, password, datacenter, validate_certs와 같은 명확한 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다.

연결이 성공적으로 설정되면, VMware 호스트만 변경할지(destination_host, VMware 호스트 vMotion) 또는 스토리지를 함께 변경할지(destination_datastore, VMware 스토리지 vMotion) 지정할 수 있습니다. 또한, 보다 복잡한 시나리오는 destination_datacenter, destination_cluster, destination_resourcepool, destination_datastore_cluster와 같은 매개변수를 사용하여 지정할 수 있습니다.

### **Links**

- https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_vmotion_module.html

### **Code**

저는 Ansible Playbook을 사용하여 가상 머신 **shim-ansible-node03**을 호스트 **vl03.lab.iroo.int** 에서 **vl04.lab.iroo.int** 로 이동하는 방법을 보여드리겠습니다(실행 전 상태는 그림 3-23, 실행 후 상태는 그림 3-24에서 확인할 수 있습니다). Ansible Playbook에는 VMware 인프라에 공통적으로 사용하는 변수를 포함한 **vars.yml** 파일이 있으며, 두 가지 작업이 포함되어 있습니다.

첫 번째 작업은 **myvm** VMware 가상 머신에 대한 이동 작업을 수행하고 그 결과를 **vm_info**라는 Ansible 변수에 저장합니다. 두 번째 작업은 **vm_info.running_host** Ansible 변수의 값을 화면에 출력합니다. 자세한 내용은 "VMware 가상 머신 실행 호스트 가져오기" 섹션을 참조하세요.

Ansible은 내부적으로 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고, 가상 머신이 성공적으로 시작되었는지 확인합니다.

> **vm_vmotion.yml**
> 

```yaml
---
- name: vMotion을 이용한 Live Migration
  hosts: localhost
  gather_facts: false
  vars:
    destination_host: "vl04.lab.iroo.int"
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: vMotion을 이용한 Live Migration
      vmware_vmotion:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        vm_name: "{{ vm_name }}"
        destination_host: "{{ destination_host }}"
      register: vm_info

    - name: VM이 운영 중인 host 정보
      ansible.builtin.debug:
        var: vm_info.running_host
```

> **vars.yml**
> 

```yaml
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-ansible-node03"
destination_host: "vl04.lab.iroo.int"
```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=3 changed=1
- 반환 값:
    
    ```yaml
    TASK [(vMotion 후) 현재 운영 중인 호스트] **********************************************************************************************************************************************
    ok: [localhost] => {
        "vm_info.running_host": "vl04.lab.iroo.int"
    }
    ```
    

만약 가상 머신이 대상 호스트의 VMware 포맷과 호환되지 않는 경우, 모듈은 다음 상태를 반환합니다:

- **대상 호스트**: localhost
- **명령어 결과**: ok=1 failed=1
- **반환 값**:
    
    ```yaml
    TASK [VM vmotio]
    fatal: [localhost]: FAILED! => {"changed": false, "msg": "(\"The virtual machine version is not compatible with the version of the host 'host2.vmware.example.com'.\", None)"}
    ```
    

코드 실행 후, VMware vSphere 클라이언트의 사용자 인터페이스에서 "**Summary**" 페이지의 **"Host"** 필드에 다음과 같은 결과가 표시될 것으로 예상됩니다. 그림 3-23과 3-24에서 확인할 수 있습니다.

![Screenshot 2024-08-27 at 9.51.41 AM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/522722be-bea2-4be9-bb84-612c64942682/Screenshot_2024-08-27_at_9.51.41_AM.png)

# [**20. 가상머신 Boot Device 순서 변경**](https://www.notion.so/Ansible-for-VMware-c9a3c03753b44b15abe38ba60746b62a?pvs=21)

Ansible Playbook과 **vmware_guest_boot_manager** 모듈을 사용하여 VMware 가상 머신의 부팅 장치 순서를 자동화할 수 있습니다 (실행 전 상태는 그림 3-25, 실행 후 상태는 그림 3-26에서 확인할 수 있습니다). 부팅 장치 순서를 변경하고, 부팅 장치 순서 상태를 확인하며, BIOS 설정을 활성화하는 작업은 VMware 인프라 관리자에게 지루하고 반복적인 작업입니다. 이러한 작업을 자동화함으로써 시간 절약은 물론, VMware 가상 머신의 부팅 순서를 변경할 때 발생할 수 있는 인간 오류를 방지할 수 있습니다.

## **Ansible Module vmware_guest_boot_manager**

**• community.vmware.vmware_guest_boot_manager**

Ansible 모듈 **vmware_guest_boot_manager**를 사용하여 VMware 게스트 도구 상태에 대한 정보를 수집할 수 있습니다. 이 모듈의 전체 이름은 **community.vmware.vmware_guest_boot_manager**로, 이는 VMware와 상호작용하는 모듈 컬렉션의 일부이며 커뮤니티에서 지원된다는 의미입니다. 이 모듈의 목적은 VMware 가상 머신 내의 특정 가상 머신에 대해 부팅 옵션을 관리하는 것입니다.

### **Parameters**

- hostname 문자열/port 정수/username 문자열/password 문자열/datacenter 문자열/validate_certs *boolean*: 연결 세부 정보
- **enter_bios_setup** *boolean*: BIOS 설정에 진입
- **boot_order** *list*: 부팅 장치 순서 (플로피, CD-ROM, 이더넷, 디스크)

VMware 가상 머신의 부팅 장치 순서를 변경하기 위해 **vmware_guest_boot_manager** 모듈을 사용할 때 다음 매개변수가 유용합니다. 먼저, **hostname**, **port**, **username**, **password**, **datacenter**, **validate_certs**와 같은 명확한 매개변수를 사용하여 VMware vSphere 또는 VMware vCenter와의 연결을 설정해야 합니다.

연결이 성공적으로 설정되면, **enter_bios_setup** *boolean*을 사용하여 BIOS 설정에 들어가도록 활성화할 수 있으며, **boot_order** 리스트를 통해 부팅 장치 순서를 설정할 수 있습니다. 부팅 장치 순서로는 플로피, CD-ROM, 이더넷, 디스크 등이 있으며, 시스템은 지정된 장치 순서에 따라 부팅을 시도합니다.

### Links

- https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_guest_boot_manager_module.html

### **Code**

Ansible Playbook에는 VMware 인프라에 공통적으로 사용하는 변수를 포함한 **vars.yml** 파일이 있으며, 하나의 작업（**tasks**）이 포함되어 있습니다. 내부적으로 Ansible은 Python 라이브러리를 통해 VMware API와 상호작용하여 작업을 실행하고 가상 머신의 성공적인 시작을 확인합니다.

> **vm_change_boot.yml**
> 

```yaml
---
- name: 가상머신 Boot Device 순서 변경
  hosts: localhost
  gather_facts: false
  collections:
    - community.vmware
  pre_tasks:
    - include_vars: vars.yml
  tasks:
    - name: 가상머신 Boot Device 순서 변경
      vmware_guest_boot_manager:
        hostname: "{{ vcenter_hostname }}"
        username: "{{ vcenter_username }}"
        password: "{{ vcenter_password }}"
        validate_certs: "{{ vcenter_validate_certs }}"
        name: "{{ vm_name }}"
        enter_bios_setup: true
        boot_order:
          - cdrom
          - disk
          - ethernet
```

> **vars.yml**
> 

```yaml
vcenter_hostname: "vc02.lab.iroo.int"
vcenter_datacenter: "LvDC"
vcenter_cluster: "LvCL"
vcenter_validate_certs: false
vcenter_username: "administrator@vsphere.local"
vcenter_password: "Ir00info1!"
vm_name: "shim-ansible-node03"
destination_host: "vl04.lab.iroo.int"
```

> **Inventory**
> 

```yaml
localhost
```

성공적인 실행 출력에는 다음이 포함됩니다

- 대상 호스트: localhost
- 명령 결과: ok=1 changed=1
- 반환 값:
    
    ```yaml
    TASK [VM change boot order] **********************************************************************************************************************
    changed: [localhost]
    ```
    

부팅 순서 변경 결과를 VMware 가상 머신의 BIOS 설정에서 확인할 수 있으며, VMware vSphere 웹 사용자 인터페이스의 웹/원격 콘솔을 사용하여 확인할 수 있습니다. 실행 전후의 상태는 그림 3-25와 3-26에서 확인할 수 있습니다.

![***Figure 3-25*** Before changing the boot order of the VMware virtual machine](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/51a91698-3f7a-4050-81f1-3d4a570eed52/Screenshot_2024-08-27_at_10.40.45_AM.png)

***Figure 3-25*** Before changing the boot order of the VMware virtual machine

![***Figure 3-26*** After changing the boot order of the VMware virtual machine](https://prod-files-secure.s3.us-west-2.amazonaws.com/49a7734f-8bc5-4890-a18a-01ec5fb955cd/8db5b6e7-8b42-4e72-8908-e4aa7c11431a/Screenshot_2024-08-27_at_10.43.18_AM.png)

***Figure 3-26*** After changing the boot order of the VMware virtual machine

## **Key Takeaways**

이 장에서는 VMware 인프라 자동화에 대해 깊이 탐구하며, 일상적인 작업에서 사용할 수 있는 코드 요약과 코드 샘플 조각들을 제공했습니다. 또한 Ansible을 VMware에 성공적으로 설정하고 설치하며 문제를 해결하는 과정을 명확히 설명했습니다.

이제, **community.vmware** 컬렉션의 강력한 리소스를 통해 VMware vSphere 사용자 인터페이스를 통해 수동으로 수행되던 간단하고 복잡한 VMware 반복 작업을 자동화할 수 있는 훌륭한 개요를 갖추게 되었습니다.

다음 장에서는 감사의 인사를 전하고 Ansible 자동화 여정을 계속해 나가는 방법을 정리하겠습니다.
