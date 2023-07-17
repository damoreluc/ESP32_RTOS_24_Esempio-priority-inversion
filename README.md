# ESP32_RTOS_24_Esempio priority inversion

## FreeRTOS Esercizio 24: Esempio illustrativo della inversione di priorità illimitata.

Si considerano tre task: __Task H__ ad alta priorità, __Task M__ a media priorità e __Task L__ a bassa priorità.

__Task L__ e __Task H__ utilizzano un lock per arbitrare l'accesso alla medesima risorsa condivisa.

L'inversione di priorità illimitata (_Unbouded Priority Inversion_) si verifica quando il task
con priorità media (__Task M__) interrompe il task a bassa priorità (__Task L__) che sta tenendo bloccato un mutex.

Se il __Task H__ ad alta priorità tenta di acquisire il lock, rimarrà bloccato (in cascata) fino a quando
il __Task L__ non rilascerà il lock.

Si chiama "illimitato" perché il __Task M__ può bloccare il __Task H__ per qualsiasi periodo di tempo,
poiché il __Task M__ sta bloccando il __Task L__ (che detiene ancora il mutex).