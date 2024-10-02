Ollydbg로 도움말 단축키인 F1을 눌렀을 때 지뢰의 위치가 전부 나오게 하도록 지뢰찾기의 어셈블리어를 수정해보았습니다.<br><br>

사용 프로그램 : IDA Freeware 8.3 ![1](https://github.com/user-attachments/assets/b4710610-a0b3-4616-a168-535f8e584504), Ollydbg ![2](https://github.com/user-attachments/assets/d9c5d4a2-7311-4beb-97c3-97a5a21e086f)
 <br><br>

IDA로 인터넷에서 다운받은 64비트버전 지뢰찾기를 열어서 함수명을 보고 폭탄을 보여주는 함수의 시작주소를 알아내었다.<br>
![3](https://github.com/user-attachments/assets/28b48515-586b-424a-b43c-50f20e5b7e08)<br><br>

(ShowBombs 함수)<br>
![4](https://github.com/user-attachments/assets/849c1b2d-ec90-400d-b2d4-3dd7f18f9165)<br><br><br>


IDA를 이용해 폭탄을 보여주는 함수(0x1002F80)을 알아내었으니, 함수의 인자를 체크하기 위해서 Xref 기능을 이용하였고, Functions에서 GameOver(x) 함수의 주소를 확인한 후 Ollydbg로 확인하였다.<br>
GameOver(x) : 0x100347C<br><br>

Ollydbg로 0x1002F80이 호출되는 곳을 확인해보니 PUSH를 통해 0A가 들어가는 것을 발견하였다. ShowBombs의 함수 인자가 0A이다.<br>
![5](https://github.com/user-attachments/assets/e76feb0c-fc78-4d7a-9767-ebb1cdd2fdf7)<br><br><br>


이제 F1 눌러 도움말 창을 나오게 하는 대신에 지뢰가 보이게 하기 위해 F1을 누를 때 발생되는 함수를 Ollydbg에서 strings 검색 기능으로 찾았다.<br>
![6](https://github.com/user-attachments/assets/4b9d4671-e1e9-4162-809a-3e8312ecebf2)<br><br><br>


F1을 눌러 나오는 도움 창을 띄워주는 함수의 시작 주소는 0x1003D76인데 해당 함수의 시작을 폭탄의 모습을 띄우는 함수를 호출하도록 바뀌게 한다. 즉, 함수를 호출하고 함수를 수행하지 않도록 함수 끝으로 JMP를 시켰다.<br>
![7](https://github.com/user-attachments/assets/669e8b7f-d1f2-4443-9645-f0655b7fa3fe)<br><br><br>


마지막으로 인자인 0A를 넣어주고 함수를 호출해준다. 그리고 도움 창을 띄워주는 함수를 실행시키지 않기 위해서 함수의 끝으로 JMP를 시켜준다.<br>
추가적으로, return 8은 _stdcall으로 8만큼 함수 안에서 스택을 처리한다는 뜻이니 도움 창을 띄워주는 함수를 수행시키지 않아 스택을 사용하지 않았음으로 8을 지워준다.<br><br><br>


F1을 눌렀을 때, 도움 창을 띄워주는 대신에 지뢰들의 위치가 전부 보이게 되고<br>
![8](https://github.com/user-attachments/assets/fb2f8a06-eac3-469f-be8a-402ee7a5d599)<br><br><br>


조금 힘들지만, 나머지 부분들을 클릭해주면 전문가 난이도도 쉽게 클리어 완료했다!<br>
![9](https://github.com/user-attachments/assets/fa1f0986-df00-450e-8e04-6ba2a5a1545e)



