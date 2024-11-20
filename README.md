### **Controlador PLL CB para plataforma Cybernet**  

Este projeto permite equipar um rádio CB com 40 canais com um codificador rotativo e um display OLED de 0,96" para navegar pelos canais no modo de canal, modo de frequência ou realizar a varredura dos canais. Ele adiciona canais extras acima e abaixo dos canais regulares. Foi projetado para rádios típicos com chassis Cybernet das décadas de 70 e 80, no meu caso um **Super Panther**.  

Embora o rádio tenha 40 canais, o PLL utilizado, o famoso **PLL02A**, pode lidar com até **512 canais**, mas o intervalo real depende do alcance do **VCO (Oscilador Controlado por Tensão)** do rádio. No meu caso, o intervalo utilizável com o controlador é de -40 a +90 (130 canais). Nos anos de ouro do CB, muitos rádios com 40 canais foram modificados com chaves para incluir canais "high", "super-high", "low" e "super-low". Naquela época, eu era ativo na cena CB e realizava muitas modificações para outros usuários.  

Em torno de 1981, projetei um scanner para CB e vendi o design para uma pequena loja de CB, que construiu e vendeu a solução. Era básico, mas oferecia 127 canais e a funcionalidade de varredura. Alguns anos depois, criei um novo design com mais recursos, como botões para avançar/retroceder rapidamente, mas era para uso pessoal. No final dos anos 80, o CB desapareceu e vendi meus rádios. Recentemente, quis criar um projeto barato para adicionar novamente um scanner com tecnologia moderna, e um amigo me deu um **Super Panther** em mau estado.  

---

### **Aviso Legal**  
Além da licença padrão, **uso comercial não é permitido**. No entanto, sinta-se à vontade para usar o design e o código para construir sua própria versão. O projeto é fornecido "como está", sem garantia ou responsabilidade, e o uso é por sua conta e risco. Não há risco real de invalidar a garantia do rádio, já que este projeto se destina a rádios das décadas de 70 e 80. Verifique se a modificação do rádio é legal no seu país.  

É necessário um **bom nível de conhecimento em eletrônica e/ou rádios CB** para realizar este projeto. **Não tente construir este controlador sem as habilidades adequadas**, pois você pode ter dificuldades ao soldar o expansor de portas ou, pior, danificar seu rádio.  

---

### **Design e Funcionalidades**
O controlador usa uma **ESP32-S3 Mini Zero**, uma das menores placas computacionais, mas muito poderosa.  

- **Plataforma de Desenvolvimento**:  
  O projeto é programado no **Arduino IDE** (recomendo a versão 1.xx em modo portátil). Isso permite "congelar" o ambiente com os drivers atuais, evitando problemas causados por atualizações que possam quebrar a compatibilidade.  

- **Código-Fonte**:  
  Inclui o código-fonte e vários arquivos de fontes (não todas são usadas, permitindo personalização). Muito está documentado nos comentários do código. Um array é usado para traduzir canais e frequências, respeitando lacunas (canais Alpha) e saltos misturados na tabela de frequências.  

- **Hardware**:  
  - O controlador conecta 9 pinos ao PLL para seleção de frequência, além de um sinal de detecção de bloqueio e uma conexão ao circuito de squelch.  
  - Como a ESP não tem pinos suficientes, é usado um **expansor de portas MCP23017**, conectado via barramento I2C.  
  - O PLL opera com níveis de 5V, enquanto a ESP usa 3,3V. O expansor funciona a 5V e se conecta diretamente ao PLL. O barramento I2C tem shifters de nível nas linhas SDA e SCL.  
  - Um transistor é usado em paralelo ao circuito de squelch e configurado para coletor aberto a 3,3V, permitindo a conexão direta à ESP.  
  - A alimentação do display OLED é filtrada por uma rede CRC.  

- **Fonte de Alimentação**:  
  O controlador requer uma alimentação de 5V. Usei um regulador **7805** com capacitores de desacoplamento. Embora não seja eficiente, o consumo de corrente é baixo e o nível de ruído é menor do que um conversor buck. Certifique-se de isolá-lo do chassi, pois este tem um terra diferente.  

- **Montagem do MCP**:  
  Soldar o MCP não é para iniciantes. Use bastante fluxo e uma ponta especial (como ponta oca estilo **Plato SMD flow tip**, **Pace wave** ou **mini wave tip**).  

---

### **Materiais Fornecidos**  
- **Código-fonte**: Inclui comentários detalhados e opções de personalização.  
- **Esquema e arquivos Gerber**: Para produção da PCB.  
- **Instruções de Programação**: Guia para instalação do ambiente de desenvolvimento e programação da ESP32-S3.  
- **Instruções de Montagem**: Específicas para um tipo de chassis Cybernet amplamente utilizado.  
- **Guia Básico do Usuário**: Explica como operar o controlador.  

---

### **Vídeo no YouTube**  
Assista ao vídeo do projeto: [https://youtu.be/u1AFa6-rFkU](https://youtu.be/u1AFa6-rFkU)  

---

### **Repositório Adicional**  
Confira também meu repositório com o **modulador/demodulador FM**.
