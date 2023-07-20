#https://www.agrolink.com.br
#https://www.tempoagora.com.br
#https://dolarhoje.com

class  color:  #titulo  em  negrito  e  colorido
  BOLD  =  '\033[1m'
  RED  =  '\033[91m'
  END  =  '\033[0m'

import  requests
from  lxml  import  html

import  datetime
from  datetime  import  datetime
data  =  datetime.now()
data_brasil  =  data.strftime('%d/%m/%Y')

linha  =  '--------------------------------------------------------------'
print(color.BOLD+data_brasil.center(62)+color.END)
print(linha)

webbot  =  'AmendoBot'
print(color.BOLD+color.RED+webbot.center(62)+color.END)
print(linha)
print('          Região  de  Tupã:')

import  requests
from  lxml  import  html
pagina  =  requests.post('https://www.agrolink.com.br/cotacoes/historico/sp/amendoim-com-casca-sc-25kg')
dados  =  html.fromstring(pagina.content)
preco  =  dados.xpath('//*[@class="table  table-striped  agk-cont-tb1"]/tbody/tr[2]/td[3]/text()')
preco  =  round(float(preco[0].replace(',','.')),2)
print('          Saca  de  25kg  de  amendoim    -  R$  {}'.format(preco))

import  requests
from  lxml  import  html
pagina  =  requests.get("https://dolarhoje.com")
dados  =  html.fromstring(pagina.content)
dolar  =  dados.xpath('//*[@id="nacional"]')[0].value
print('          Cotação  do  Dolar            -  R$  {}'.format(dolar))

import  json
reqApi=requests.get('https://api.tempoagora.com.br/forecast?city=Tupa-SP')
jsonApi=json.loads(reqApi.content.decode('utf-8'))
print  ('          Precipitação:              -  ',  jsonApi['list'][0]['precipitation'],  '  mm')
precitacao=  jsonApi['list'][0]['precipitation']
print(linha)

import  csv
with  open('dados_amendoim.csv',  'a',  newline='')  as  arquivo:
  final  =  csv.writer(arquivo,  delimiter=';')
  #final.writerow(['  Saca  de  25kg  de  amendoim',  '  Cotação  do  Dolar',  '  Precitação'])
  final.writerow([preco,  dolar,  precitacao])

import  pandas  as  pd
arquivodf  =  pd.read_csv('dados_amendoim.csv',  sep=';')
print(arquivodf)
print(linha)