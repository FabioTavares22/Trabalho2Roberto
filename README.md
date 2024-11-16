---
marp: true
theme: gaia
---

# Definições
-
    Neste trabalho falaremos sobre a estratégia de tratamento de erros. No desenvolvimento de sistemas precisamos prever que existem falhas e precisamos nos preparar para lidar com essas falhas, evidentemente não conseguimos englobar todos os cenários e alguns também que são englobados podem nunca ocorrer. O ponto é que a estratégia de tratamento pode se tornar um problema maior do que a própria falha que estamos tratando ou até mesmo não ser um problema em si mas quando for ativada nos causar um problema, neste trabalho falarei sobre a estratégia de fallback.
---
# Conceito e Funcionamento
-
    O fallback consiste na utilização de um mecanismo diferente para alcançar o mesmo resultado, por exemplo, vamos imaginar um caixa eletrônico de um banco que aceita depósitos como já conhecemos colocamos todo dinheiro em um envolope e iniciamos o depósito onde o caixa faz a contagem das cédulas e nos emite o comprovante agora vamos pensar que por algum motivo houve uma falha na contagem dessas cédulas e agora para realizarmos um depósito precisamos inserir no caixa cédula por cédula e a cada inserção temos um comprovante de depósito. Vemos que o processo de inserir uma cédula por vez resolve o problema dos depósitos permitindo que estes continuem mas ele traz o grande incômodo da inserção única e provavelmente trará mais transtornos como filas para realizar depósitos, depósitos que eram feitos rapidamente para serem computados no mesmo expediente bancário agora não são mais computados devido a demora dentre outras coisas.
---
# Aplicabilidade
-
    O fallback é aplicável quando queremos realizar um tratamento para um erro que podemos ter, por exemplo, podemos realizar a conexão com uma API para realizarmos o envio de dados mas ao realizarmos a chamada obtemos como resposta um erro 400 que indica que o servidor não foi encontrado neste caso poderíamos simplesmente aguardar um tempo e realizarmos novamente a chamada. Um exemplo de fallback que poderia ser implementado neste caso seria não realizar nenhuma chamada mais já que o erro indica que o servidor não foi encontrado mas veja que neste caso teríamos um problema se o erro fosse apenas por uma indisponibilidade temporária do servidor.
---
# Casos de uso
-
    Vamos para um exemplo prático onde a estratégia de tratamento pode se tornar pior do que um preparo em código para lidarmos com o erro. Este caso é real e o fallback não foi implementado só iremos imaginar que este tenha sido.
    Abaixo temos uma imagem de um erro, este erro foi causado porque ao inserirmos dados no banco de dados algumas informações que inicialmente são obrigatórias não se encontravam preenchidas:
    <img src="/Imagem 1.png" alt="Erro de Inserção">
    A sugestão para tratamento seria criarmos um botão que permitisse que após a correção das informações esse arquivo pudesse ser reprocessado, entretanto temos diversos problemas com esse tratamento de erro como por exemplo a inserção de um arquivo desatualizado, o sistema deixaria de realizar novos downloads até que este arquivo fosse processado, ainda que as informações fossem corrigidas o download seria desativado até que este processamento fosse feito e teríamos também o risco de sobrepor um download mais atualizado após as correções.
    O principal ponto que torna este fallback inviável é que estamos falando de um sistema que tem vários usuários que podem executar a tarefa de reprocessamento simultaneamente causando assim vários problemas.
    A sugestão de tratamento não foi implementada e seguimos com o tratamento implementado desde o início que consiste em apresentar o erro, permitir que o usu´rio faça as correções e automaticamente realizar o download no horário programado e inserir o arquivo novamente, caso os erros tenham sido corrigidos a inserção ocorre com sucesso mas se não foram corrigidos serão novamente exibidos em tela.
---
# Conclusão
-
    Podemos concluir que, quando realizamos o desenvolvimento devemos prever e tratar os possíveis erros que teremos de maneira que esse tratamento não se torne um problema.
    No caso de exemplo dado acima a implementação de um fallback que consiste numa maneira diferente de chegar ao mesmo resultado poderia trazer muitos problemas como por exemplo a inserção de informações incorretas no sistema, em princípio a ideia parece ser um ótimo tratamento para os erros apresentados mas quando analisamos um pouco mais seus possíveis resultados acabamos por perceber que ela é mais problemática do que solucionadora.
    Evidentemente alguns problemas apresentados pela sua implementação podem também serem corrigidos ou evitados mas perceba que a implementação deste fallback torna o processo de correção e de lida com erros mais caro e mais trabalhoso do que simplesmente abrodar o processo, exibir os erros em tela, permitir que o usuários os corrija e refazer a inserção das informações.
    Enfim, o processo de tratamento de erros no desenvolvimento e implementação de sistemas não é uma tarefa fácil e tão pouco pequena mas devemos sempre pensar se ao implementarmos uma medida de lida com erros se teremos de fato uma solução com aquela implementação ou se teremos problemas ainda maiores do que o o original.
---