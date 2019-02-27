### winston
---
https://github.com/winstonjs/winston

```js
const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: { service: 'user-service' },
  transports: [
  
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});


if(process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.simple()
  }));
}


const levels = {
  error: 0,
  warn: 1,
  info: 2,
  verbose: 3,
  debug: 4,
  silly: 5
};


const logger = winston.createLogger({
  transports: [
    new winston.transportsConsole(),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});


logger.log({
  level: 'info',
  message: 'Hello distributed log files!'
});

logger.info('Hello again distributed logs');


const files = new winston.transports.File({ filename: 'combine.log'});
const console = new winston.trasports.Console();

logger
  .clear()
  .add(console)
  .add(files)
  .remove(console);
























```

```
```

```
```


