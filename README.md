# LINA_AI_Agent_research


## 1. Claude 설치

#### 1) 공식 Native Install 설치

<pre><code>curl -fsSL https://claude.ai/install.sh | bash</code></pre>

#### 2) 설치 후 터미널을 종료 후 다시 확인

<pre><code>claude --version</code></pre>

<img width="559" height="297" alt="image" src="https://github.com/user-attachments/assets/22c6a185-c437-40cb-8916-2fa4698f4917" />


#### * 터미널이 claude 명령어 위치를 못 찾는 상태

##### 1) 쓰기권한 추가

###### 1. .zshrc 권한 확인

<pre><code>ls -l ~/.zshrc</code></pre>

루트 소유자
<img width="465" height="32" alt="image" src="https://github.com/user-attachments/assets/1dbdc431-b924-47a7-9f21-3b6091ab445c" />

###### 2. 소유권을 내 계정으로 변경

<pre><code>sudo chown "$USER":staff ~/.zshrc chmod u+w ~/.zshrc</code></pre>

###### 3. 다시 PATH 추가

<pre><code>echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc source ~/.zshrc</code></pre>

###### 4. 설치 확인

<pre><code>claude --version</code></pre>

정상
<img width="465" height="32" alt="image" src="https://github.com/user-attachments/assets/d0078fee-7816-4291-81e8-178d9fde9854" />

###### 5. 실행

<pre><code>claude</code></pre>

<img width="560" height="559" alt="image" src="https://github.com/user-attachments/assets/31c056f9-cadc-4641-919b-12da2dd1aff3" />



<pre><code>
↑ ↓ 방향키 : 선택 이동

Enter : 선택 확정

Ctrl + C : 종료
</code></pre>


###### 6. 로그인인증


<img width="558" height="179" alt="image" src="https://github.com/user-attachments/assets/006eccd3-89a3-4172-a9b3-541b14b3f6e8" />


<img width="690" height="278" alt="image" src="https://github.com/user-attachments/assets/5e72e7f3-53cd-4ab1-aab4-63b569943d50" />


###### 7. /init
<p>Claude Code가 현재 폴더 구조를 보고 CLAUDE.md 같은 작업 가이드 파일을 만들 수 있음</p>


<img width="688" height="358" alt="image" src="https://github.com/user-attachments/assets/b6d58d64-3cca-4f52-a391-30ae5de57003" />






