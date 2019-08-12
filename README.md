# Rol de ansible para la generacion de los tickscripts


Tiene 5 partes:
 - Busca el archivo /srv/sensor/VolumenCompartido/networking.yml de donde recibe los datos dispositivos/alarmas e instancias para generar alarmas
 - Usando un template, itera sobre los items en networking.yml, y crea un .yaml para cada uno con nombre (dispositivo)-(nombre del dispositivo)-(instancia).yaml
 - Guarda los datos de los scripts que genero
        Si algun script quedo en blanco(no se encontro el modelo/instancia con los parametros), se guarda en un archivo: notFoundScripts.log con el nombre (dispositivo)-(nombre del dispositivo)-(instancia).yaml, de todos los scripts que tuvieron ese problema.
        Luego se eliminan estos archivos
 - Habilita los scripts en kapacitor
 - Corre un comando de influx para cada metrica que tiene una alarma y crea un cq para guardar el dato por 1 año


 - Los logs de ejecucion de ansible se guardan en un archivo ansible.log


TODO
 X Crear un log para cada alarma que queda en blanco
 X Que permita elegir si los scripts son batch o stream
 X Que influxdb guarde por 1 año los datos
