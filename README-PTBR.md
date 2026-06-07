# Intermediate Nmap - Write-up TryHackMe

## Enumeração

A enumeração inicial foi realizada utilizando o Nmap para identificar portas abertas e possíveis vetores de ataque.

```bash
nmap <IP> -sS -sC -sV 
```

Ao executar o scan, encontramos algumas portas altas abertas na máquina alvo.

O parâmetro `-sC` executa os scripts padrão do NSE (Nmap Scripting Engine), permitindo coletar informações adicionais sobre os serviços encontrados, como títulos de páginas web, compartilhamentos SMB, certificados SSL e outras informações úteis.

Já o parâmetro `-sV` realiza a detecção de versões dos serviços, identificando exatamente o software que está sendo executado em cada porta aberta.

Através da enumeração inicial, já foi possível identificar uma anotação contendo possíveis credenciais: <br><br> <img width="924" height="566" alt="image" src="https://github.com/user-attachments/assets/d3ca1430-bf05-4c62-a4b7-649235fa46fc" /> <br><br>

## Enumeração Web

Ao acessarmos a aplicação web disponível na porta `31337`, encontramos as mesmas credenciais expostas na página: <br><br> <img width="1002" height="291" alt="image" src="https://github.com/user-attachments/assets/f819c7ff-fd19-4a89-af11-67e030d65a11" /> <br><br>

## Acesso Inicial

Com as credenciais obtidas durante a enumeração, tentamos autenticação via SSH e conseguimos acesso à máquina com sucesso: <br><br> <img width="759" height="454" alt="image" src="https://github.com/user-attachments/assets/b15fa2ba-d3a9-48e5-9dbe-d43b80365bb3" /> <br><br>

## Flag de Usuário

Após obter acesso inicial, retornamos para o diretório `/home` para continuar a enumeração do sistema.

Durante a análise, identificamos o usuário `user`. Ao acessar seu diretório, encontramos a flag de usuário: <br><br> <img width="511" height="192" alt="image" src="https://github.com/user-attachments/assets/8a783a15-f3ff-42b6-9c0d-6c1eb396c1b3" /> <br><br>

```text
flag{25f1309497a18888dde5222761ea88e4}
```

## Conclusão

A máquina demonstrou a importância de uma enumeração cuidadosa. Através de um simples scan de serviços e da análise da aplicação web exposta em uma porta não convencional, foi possível obter credenciais válidas, realizar acesso via SSH e capturar a flag de usuário.

## Remediação

Para evitar que esse tipo de comprometimento ocorra em ambientes reais, algumas medidas de segurança devem ser adotadas:

* **Não armazenar credenciais em arquivos acessíveis publicamente**, páginas web ou diretórios sem proteção adequada.
* **Restringir o acesso a serviços expostos em portas não convencionais**, garantindo que apenas usuários autorizados possam acessá-los.
* **Aplicar o princípio do menor privilégio**, limitando o acesso dos usuários apenas aos recursos necessários para suas funções.
* **Utilizar senhas fortes e exclusivas**, evitando reutilização de credenciais entre diferentes serviços.
* **Implementar autenticação multifator (MFA)** sempre que possível, especialmente para acessos remotos como SSH.
* **Realizar auditorias periódicas** para identificar informações sensíveis expostas em aplicações web e sistemas.
* **Monitorar tentativas de acesso e atividades suspeitas**, permitindo a detecção precoce de possíveis comprometimentos.
* **Manter sistemas e serviços atualizados**, reduzindo a superfície de ataque e corrigindo vulnerabilidades conhecidas.

A exposição de credenciais foi o principal vetor de comprometimento desta máquina. A adoção dessas práticas reduziria significativamente o risco de acesso não autorizado ao ambiente.
