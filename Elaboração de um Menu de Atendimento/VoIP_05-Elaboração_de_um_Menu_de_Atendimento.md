# VoIP 05 - Elaboração de um Menu de Atendimento


## Crie na sua central Asterisk um menu de atendimento acessível no número NN05 (NN= identificador do seu container) com as seguintes opções:

Mensagem inicial: "Após o fim desta mensagem, digite 1 para gravar um áudio, 2 para escutar o áudio gravado, 3 para escutar meu nome completo ou 0 para sair". Se nenhuma opção for digitada pelo usuário até 10s após o fim da mensagem inicial, ela deverá ser repetida. Se uma opção inválida for fornecida, a mensagem "Opção inválida" será informada e o menu repetido.

Para fonalizar a mensagem inicial, use a aplicação Espeak, instalada no seu Asterisk, da seguinte forma:

Espeak("Mensagem de texto",any) - Lembre de por a extensão e a prioridade conforme visto em sala.

(O Espeak apenas "lê" a mensagem de texto que lhe é repassada como parâmetro, mas não coleta as escolhas digitadas pelo usuário. Isso será feito apenas pela aplicação Waitexten. Nesta primeira atividade, não usaremos a Background, motivo pelo qual as opções do usuário só serão coletadas pela Waitexten APÓS a mensagem "lida" pelo Espeak)

Já para gravar o áudio, use a aplicação Record, conforme abaixo:

Record(filename:format,[silence,[maxduration,[options]]]) - Lembre de por a extensão e a prioridade conforme visto em sala.

Exemplo: 
~~~
Record(//caminho//pasta//gravacao//arquivo_de_som:gsm)
~~~

Use o "#" para concluir a gravação

Instruções adicionais: https://wiki.asterisk.org/wiki/display/AST/Asterisk+13+Application_Record

Por fim, para escutar o áudio, use a aplicação PlayBack, já vista em sala.

Exemplo: 
~~~
PlayBack(arquivo_de_som)
~~~
Veja o exemplo a seguir de uma extensão que usa estas aplicações:
~~~
exten => 300,1,Answer()
same => n,Espeak("Grave o seu som a seguir", any)
same => n,Record(//var//lib//asterisk//sounds//pt_BR//som:gsm)
same => n,PlayBack(som)
same => n,Wait(3)
same => n,Hangup()
~~~

Dica:

Faça primeiro as opções "1" e "2" do menu de atendimento. Depois utilize-as para gravar um arquivo de som com o seu nome completo, que será utilizado na opção "3", assim como a mensagem de som "opção inválida", ambos gravados com a sua própria voz. Ao terminar cada gravação, renomeie o arquivo para utilizá-lo no Playback que tratará a opção em questão (opção "3" ou opção inválida). Não deixe com o mesmo nome que foi originalmente gerado, pois o arquivo será sobreposto na próxima vez que for selecionada a opção "1" do Menu.

Teste a sua extensão e quando estiver de acordo com o solicitado.



