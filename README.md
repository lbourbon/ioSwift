# ioSwift

### Novo Projeto
Organization Identifier: com.[nome da empresa]


### MVC
Model View Controller é um padrão de arquitetura de software

Model é a estrutura que controla os dados, mas não é o próprio dados. Manipula e lê dados.
Controller é a comunicação entre o Model e o View. Troca dados com o Model e envia dados para o View
View é a camada de interação com o usuário. É utilizada para receber a entrada de dados e apresentar visualmente o resultado.
No projeto do XCode, criar 3 pastas com cada nome e colocar dentro das pastas:
Model: SeuModel.swift; SeuBancoDeDados.swift
View: Main.storyboard; Images.xcasset
Controller: AppDelegate.swift; ViewController.swift


### Criar App Icon
www.canva.com para desenhar seu ícone
clica em custom dimension (1024x1024)
download como PNG

www.appicon.co para modificar para múltiplas dimensões
arrastar imagem gerada
escolher os dispositivos

no Xcode botão direito em Asses.Xcassets
apagar a pasta AppIcon.appiconset e colocar sua baixada de appicon.co


## UI Elements

### Constrains
Duas formas de criar restrições: pinning(fixação) ou alignment(alinhamento)

#### Pinning
Fixamos as bordas do objeto em relação as bordas da tela (ou outros objetos próximos), o tamanho é determinado dinamicamente, pela fórmula:
* width: tela.width - (x + x) , onde x é a distância da borda do objeto até as bordas da tela
* height: tela.height - (y + y) , onde y é a distância da borda do objeto até as bordas da tela

#### Alignment
Fixamos o tamanho do objeto (width e height) e decidimos o alinhamento (ex: centro da tela ou centro de alguma subview),
a distância para as bordas serão determinadas dinamicamente, pela fórmula (no caso do objeto no centro da tela):
* x: tela.width/2 - width/2
* y: tela.height/2 - height/2

-> PINNING NA PRÁTICA: o tamanho do objeto vai variar a depender do tamanho da tela do telefone.
- Clicar no botão Add New Constrains
- Remover fixar da margem: faz com que fixe a partir da borda da tela e não deixa margem
- Escolher distâncias 
- Add Constrains

-> ALIGNMENT NA PRÁTICA: mesmo tamanho para todas as telas, mas a distância para os outros objetos varia.
- Clicar no botão Constrains
- Clicar em width e height (para fixar tamanho)
- Clica no botão Align
- Escolhe alinhamento

-> DICA: ADICIONAR OBJETOS DENTRO DE CONTAINERS (UIViews) PARA FACILITAR ALINHAMENTO. (ex: 3 containers, os de baixo e de cima fixados nas margens e no do meio. O do meio alinhado no centro)

-> REMOVER CONTRAINS: Clica em Resolve Auto Layout Issues; Clear Constrains

-> IPHONE X: 1. Change the canvas to iPhone Xs. 2. Select the background view 3. With the background still selected, go to the size inspector and double click on the constraint that's called "Bottom Space to". 4. Change the first dropdown to Superview and the constant to 0.


#### Programaticamente
Criar um objeto square a ser localizado no centro da tela, independente do tamanho:
```
let square = UIView(frame: CGRect(x:self.view.frame.width/2 - self.width/2, y:self.view.frame.height/2 - self.height/2, width:100, height:100))
self.view.addSubview(square)
```

### Optionals
Em algumas ocasiões podemos querer que as variáveis possam tem valor **nil**. Para isso usamos optionals
A interrogação quer dizer: a variável nome pode ser **String** ou **nil**
```
let nome: String?
```
Se usar a variável sem ter inicializado, ocorrerá erro
A exclamação (_force unwrapping_) seria o programador dizendo: pode rodar o programa que eu garanto que a variável tem valor<br>
```print(nome!)```  erro de ponteiro nulo
<br>
para contornar esse erro pode ser usado:
```
if nome != nil
print(nome)
```
ou melhor: usar um _optional binding_
```
if let nomeCadastrado = nome
print(nome)
```

### Segue

### Cocoapods
Instalar: (terminal) 
> sudo gem install cocoapods
> pod setup --verbose

Add cocoapods no projeto: fecha xcode, na pasta do proj. 
no terminal:
> pod init (cria o podfile)
> open -a Xcode Podfile (abre o podfile no xcode)
- uncomment next line
- adiciona pods no bloco do-end: pod 'NomeDoPod'
> pod install
- A partir daqui trabalhar com o .xcworkspace
