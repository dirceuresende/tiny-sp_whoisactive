Por diversas vezes, já tive problemas de lentidão ao executar a sp_WhoIsActive em ambientes com alto processamento e contenção de disco e/ou TempDB, fazendo com que o retorno da SP demorasse vários segundos, até mesmo alguns minutos, uma vez que essa SP tem muita utilização de TempDB para retornar os resultados da forma que ela retorna atualmente.

Com o objetivo de prover uma solução parecida com a sp_WhoIsActive, mas que fosse mais leve e não utilizasse a TempDB, permitindo que ela seja executada rapidamente mesmo em cenários como o citado acima, eu e o <a href="https://www.tiagoneves.net/blog/">Tiago Neves</a> criamos essa versão mais "enxuta", retornado as principais informações e sem utilizar os diversos parâmetros que a SP original nos fornece.

<h2>Qual a diferença para a sp_WhoIsActive?</h2>
<ul>
<li>Não utiliza a TempDB</li>
<li>Execução mais rápida</li>
<li>Código mais simples de entender</li>
<li>Pode ser facilmente utilizada como view, table-valued function ou scalar function, permitindo utilizar order by, select into, where, etc.</li>
<li>Além de mostrar a query em execução, mostra também o Outer Command (a sp_WhoIsActive também mostra se utilizado o parâmetro @get_outer_command = 1)</li>
<li>Caso a sessão seja de um job, mostra o nome do job na coluna program_name</li>
<li>Retorna o XML do plano de execução (a sp_WhoIsActive também mostra se utilizado o parâmetro @get_plans = 1)</li>
</ul>

Veja mais sobre essa SP também no meu artigo sobre ela, acessando o link <a href='https://www.dirceuresende.com/blog/sql-server-query-para-retornar-as-sessoes-ativas-sp_whoisactive-sem-consumir-tempdb/'>SQL Server - Query para retornar as consultas em execução (sp_WhoIsActive sem consumir TempDB)</a>
