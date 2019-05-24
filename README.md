# ioSwift

## Novo Projeto
Organization Identifier: com.[nome da empresa]

## MVC
Model View Controller é um padrão de arquitetura de software

Model é a estrutura que controla os dados, mas não é o próprio dados. Manipula e lê dados.
Controller é a comunicação entre o Model e o View. Troca dados com o Model e envia dados para o View
View é a camada de interação com o usuário. É utilizada para receber a entrada de dados e apresentar visualmente o resultado.
No projeto do XCode, criar 3 pastas com cada nome e colocar dentro das pastas:
Model: SeuModel.swift; SeuBancoDeDados.swift
View: Main.storyboard; Images.xcasset
Controller: AppDelegate.swift; ViewController.swift


## Criar App Icon

www.canva.com para desenhar seu ícone
clica em custom dimension (1024x1024)
download como PNG

www.appicon.co para modificar para múltiplas dimensões
arrastar imagem gerada
escolher os dispositivos

no Xcode botão direito em Asses.Xcassets
apagar a pasta AppIcon.appiconset e colocar sua baixada de appicon.co

## Constrains



## Cocoapods
instalar: terminal > sudo gem install cocoapods
                  > pod setup --verbose
adic cocoapods no projeto: fecha xcode,
na pasta do proj. no terminal > pod init (cria o podfile)
> open -a Xcode Podfile (abre o podfile no xcode)
- uncomment next line
- adiciona pods no bloco do-end: pod 'NomeDoPod'
> pod install
- A partir daqui trabalhar com o .xcworkspace
