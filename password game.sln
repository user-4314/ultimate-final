INCLUDE Irvine32.inc

.data 
key sdword ?
lowedge dword 1
highedge dword 100
lifeleft byte "剩餘猜題次數:",0
higher byte "再高一點    ",0
lower byte "再低一點    ",0
correct byte "恭喜答對!!!!!!!!",0
wrongrange byte "錯誤的輸入請重新輸入",0
input byte "請輸入數字1到100:",0
inputagain byte "請輸入數字",0
inputagain1 byte "到",0
inputagain2 byte ": ",0
endgame byte "猜題次數已用完遊戲結束",0
rule byte "                    規則:你只有十次機會可以猜對答案",0

.code
main PROC   
     call   Randomize                   ;隨機取一個1到100的數字當做答案
     mov  eax,100
     call RandomRange
     mov  key,eax                       ;將亂數設定為答案
     mov ecx,10                         ;設定遊戲次數為10
    
     mov   eax , yellow + ( black*16 )  ; 顯示黃字
     call   SetTextColor
     mov edx,offset rule                ;顯示規則信息
     call WriteString	
     call CRLF
     call CRLF
     mov   eax , white + ( black*16 )   ; 調回白色 
     call   SetTextColor

     mov edx,offset input               ;顯示輸入信息
     call WriteString	
     call CRLF

     call readdec                       ;讀取使用者鍵盤資料

     .while eax!=key                    ;使用者沒猜到答案就重複執行

        .if eax>key && eax<=highedge    ;當輸入比答案高時的情況
            mov edx,offset lower
            call WriteString	 
            dec ecx
            mov highedge ,eax           ;把使用者輸入資料設為下次猜數字的最高範圍
            
       .elseif  eax<key && eax>=lowedge  ;當輸入比答案低時的情況
            mov edx,offset higher
            call WriteString	 
            dec ecx
            mov lowedge ,eax            ;把使用者輸入資料設為下次猜數字的最低範圍
            
        .elseif  eax<=lowedge || eax>highedge  ;當輸入字串、符號、超過範圍時就會顯示錯誤的信息
            mov   eax , blue + ( black*16 )    ; 顯示藍字
            call   SetTextColor
            mov edx,offset wrongrange
            call WriteString
            mov   eax , white + ( black*16 )    ; 調回白色
            call   SetTextColor
            call CRLF
            call CRLF
            
        .endif

        .if ecx==0                      ;當使用者猜的次數達到十次會結束遊戲
            call CRLF
            mov   eax , red + ( black*16 )    ;顯示紅字
            call   SetTextColor
            mov edx,offset endgame             
            call WriteString	 
            call CRLF
            exit

        .else
            mov edx,offset lifeleft      ;告訴使用者還剩多少猜題次數
            call WriteString	
            mov eax,ecx
            call writedec
            call CRLF
            call CRLF

            mov edx,offset inputagain     ;次數未達10次會顯示輸入信息給使用者繼續猜
            call WriteString	 
            mov eax,lowedge               ;提示使用者這輪的範圍在哪
            call writedec
            mov edx,offset inputagain1         
            call WriteString
            mov eax,highedge
            call writedec
            mov edx,offset inputagain2         
            call WriteString
            
            call readdec

        .endif

     .endw

        call CRLF                       ;使用者輸入與答案相符時情況
        mov   eax , green + ( black*16 )    
        call   SetTextColor
        mov edx,offset correct           
        call WriteString	 
        call CRLF
        exit

main ENDP
END main
