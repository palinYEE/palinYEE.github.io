---
layout: post
title:  "[PYTHON] 하위 디렉토리에 있는 해시를 읽어와서 virustotal에 질의 후 엑셀에 저장하자. "
date:   2021-01-11T18:09:52-05:00
author: 윤영진
categories: python
tags: python virustotal excel
cover:  "/assets/instacode.png"
---
## 목적

이 포스터는 간단하게 코드를 구현한 내용이다. 이 코드를 해석하면 파이썬의 다음 세가지를 학습할 수 있을 것이다. 

* 파이썬을 이용해서 엑셀 작성하기
* virustotal api 이용하기
* `glob()` 함수를 사용하기

이 코드를 실행하는데 하나의 전제조건이 필요하다. 이는 바로 다음과 같은 구성의 디렉토리가 존재해야 한다는 것이다. 

* `[아무 디렉토리] / [파일의 해시값] / 파일`

ex) y/y/j/12345656788242sdsd/yyj.exe

## 코드 만든 이유

위와 같은 디렉토리가 많을 때 자동으로 이를 스캔하고 virustotal에 질의한 후, 엑셀에 자동으로 저장해주는 코드가 필요했다.  

<pre>
<code>
import requests, json
from openpyxl import Workbook
from glob import glob

if __name__ == "__main__":
    api_key = "[api key 입력]"
    v_url = 'https://www.virustotal.com/vtapi/v2/file/report'

    malware_list = []

    write_wb = Workbook()
    write_ws = write_wb.active
    write_ws['A1'] = '파일 명'
    write_ws['B1'] = '경로'
    write_ws['C1'] = 'md5'
    write_ws['D1'] = 'sha1'
    write_ws['E1'] = 'sha256'
    write_ws['F1'] = 'Antivirus results'
    
    count = 2

    file_list = glob('[경로 입력]')      # path 입력
    for file in file_list:
        data_frame = {"path":"", "file_name":"", "file_hash":""}
        for sub_path in file.split('/')[:-1]: data_frame["path"] += sub_path + '/'
        data_frame["file_name"] = file.split('/')[-1]
        data_frame["file_hash"] = file.split('/')[-2]
        malware_list.append(data_frame)


    for malware in malware_list:
        
        params = {'apikey' : api_key, 'resource' : malware["file_hash"]}
        response = requests.get(v_url, params=params).json()
        if response["verbose_msg"] == "Scan finished, information embedded":
            write_ws[f'A{count}'] = malware['file_name']
            write_ws[f'B{count}'] = malware['path']
            write_ws[f'C{count}'] = response['md5']
            write_ws[f'D{count}'] = response['sha1']
            write_ws[f'E{count}'] = response['sha256']
            virus_str = ''
            for key, value in response['scans'].items():
                if value['detected']: virus_str += f'{key}/{value["result"]}\n'
            write_ws[f'F{count}'] = virus_str
            count += 1

        # print(json.dumps(response,indent=4))

    write_wb.save('malware_virustotal_info.xlsx')
</code>
</pre>