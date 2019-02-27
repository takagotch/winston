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


const logger = winston.createLogger({
  level: 'info',
  transports: [
    new winston.transports.Console(),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});


const DailyRotateFile = require('winston-daily-rotate-file');
logger.configure({
  level: 'verbose',
  transports: [
    new DailyRotateFile(opts)
  ]
});


const logger = winston.createLogger({
  transports: [
    new winston.tranports.Console(),
  ]
});

const childLogger = logger.child({ requestId: '451' });


const info = {
  level: 'info',
  message: 'Hey! Log something?'
};

const { level,message, ...meta } = info;


const { LEVEL, MESSAGE, SPLAT } = require('triple-beam');

console.log(LEVEL === Symbol.for('level'));

console.log(MESSAGE === Symbol.for('message'));

console.log(SPLAT === Symbol.for('splat'));


logger.log('error', 'hello', { message: 'world' });
logger.info('hello', { message: 'world' });


const { createLogger, format, transports } = require('winston');
const { combine, timestamp, label, printf } = format;

const myFormat = printf(({ level, message, label, timestamp }) => {
  return `${timestamp} [${label}] ${level}: ${message}`;
});

const logger = createLogger({
  format: combine(
    label({ label: 'right meow!' }),
    timestamp(),
    myFormat
  ),
  transports: [new transports.Console()]
});


const { createLogger, format, transports } = require('winston');
const { combine, timestamp, label, prettyPrint } = format;

const logger = createLogger({
  format: combine({
    lable({ label: 'right meow!' }),
    timestamp(),
    prettyPrint()
  }),
  transports: [new transports.Console()]
})

logger.log({
  level: 'info',
  message: 'What time is the testing at?'
});


const { createLogger, format, transports } = require('winston');
const logger = createLogger({
  format: format.combine(
    format.splat(),
    format.simple()
  ),
  transports: [new transports.Console()]
});

logger.log('info', 'test message %s', 'my string');

logger.log('info', 'test message %d', 123);

logger.log('info', 'test message %s, %s', 'first', 'second', { number: 123 });


const { createLogger, format, transports } = require('winsotn');

const ignorePrivate = format((info, opts) => {
  if (info.private) { return false; }
  return info;
});


const logger = createLogger({
  format: format.combine(
    ignorePrivate(),
    format.json()
  ),
  transports: [new transports.Console()]
});

logger.log({
  level: 'error',
  message: 'Public error to share'
});

logger.log({
  private: true,
  level: 'error',
  message: 'This is super secret - hide it.'
});


const { format } = require('winston');
const { combine, timestamp, label } = format;

const willNeverThrow = format.combine(
  format(info => { return false })(),
  format(info => { throw new Error('Never reached') })()
);


const { format } = require('winston');

const valume = format((info, opts) => {
  if (opts.yell) {
    info.message = info.message.toupperCase();
  } else if (opts.whisper) {
    info.message = info.message.toLowerCase();
  }
  
  return info;
});

const scream = volume({ yell: true });
console.dir(scream.transform({
  level: 'info',
  message: `sorry for making you YELL in your head!`
}, scream.options));

const whisper = volume({ whisper: true });
console.dir(whisper.transform({
  level: 'info',
  message: `WHY ARE THEY MAKING US YELL SO MUCH!`
}, whisper.options));


logger.log('silly', "127.0.0.1 - there's no place like home");
logger.log('debug', "127.0.0.1 - there;s no place like home");

winston.log('info', "127.0.0.1 - there's no place like home");
winston.info("127.0.0.1 - there's no place like home");


const logger = winston.createLogger({
  levels: winston.config.syslog.levels,
  transports: [
    new winston.transports.Console({ level: 'error' }),
    new winston.transports.File({
      filename: 'combined.log',
      level: 'info'
    })
  ]
});


const transports = {
  console: new winston.transports.Console({ level: 'warn' }),
  file: new winston.transports.File({ filename: 'combined.log', level: 'error' })
};

const logger = winston.createLogger({
  transports: [
    transports.console,
    transports.file
  ]
});

logger.info('Will not be logged in eigher transpot!')
transports.console.level = 'info';
transports.file.level = 'info';
logger.info('@ill be logged in both transports!');


const myCustomLevels = {
  levels: {
    foo: 0,
    bar: 1,
    baz: 2,
    foobar: 3
  },
  colors: {
    foo: 'blue',
    bar: 'green',
    baz: 'yellow',
    foobar: 'red'
  }
};

const customLevelLogger = winston.createLogger({
  levels: myCustomLevels.levels
});

customLevelLogger.foobar('some foobar level-ed message');


winston.addColors(myCustomevels.colors);

winston.format.combine(
  winston.format.color(),
  winston.format.json()
);


const logger = winston.createLogger({
  transports: [
    new winston.transports.File({
      filename: 'combined.log',
      level: 'info'
    }),
    new winston.transports.File({
      filename: 'errors.log',
      level: 'error'
    })
  ]
});


const combinedLogs = logger.transports.find(transport => {
  return transport.filename === 'combined.log'
});

logger.remove(combinedLogs);


const Transport = require('winston-transport');
const util = require('util');

module.exports = class YourCustomTransport extends Transport {
  constructor(opts) {
    super(opts);
  }
  
  log(info, callback) {
    setImmediate(() => {
      this.emit('logged', info);
    });
    
    callback();
  }
};


const { createLogger, transports } = require('winston');

const logger = createLogger({
  transports: [
    new transports.File({ filename: 'combined.log' })
  ],
  exceptionHandlers: [
    new tranports.File({ filename: 'exceptions.log' })
  ]
});

const logger = createLogger({
  transports: [
    new transports.File({ filname: 'combined.log' })
  ]
});

logger.exceptions.handle(
  new transports.File({ filename: 'exception.log' })
);


winston.exception.handle(
  new winston.transports.File({ filename: 'path/to/exceptions.log' })
);

winston.add(new winston.transports.File({
  filename: 'path/to/combined.log',
  handleExceptions: true
}));


const logger = winston.createLogger({ exitOnError: false });
logger.exitOnError = false;


const logger = winston.createLogger({
  transports: [
    new winston.transports.File({ filename: 'path/to/combined.log' })
  ],
  exceptionHandlers: [
    new winston.transports.File({ filename: 'path/to/exceptions.log' })
  ]
});


const logger = winston.createLogger({
  transports: [
    new winston.transports.Console({
      handlerExceptions: true
    })
  ],
  exitOnError: false
});


function ignoreEpipe(err) {
  return err.code !== 'EPIPE';
}

const logger = winston.createLogger({ exitOnError: ignoreEpipe });

logger.exitOnError = ignoreEpipe;


logger.profile('test');

setTimeout(function () {
  logger.profile('test');
}, 1000);


const profiler = logger.startTimer();
setTimeout(function () {
  profiler.done({ message: 'Logging messsage' });
}, 1000);


logger.profile('test', { level: 'debug' });



const options = {
  from: new Date() - (24 * 60 * 60 * 1000),
  until: new Date(),
  limit: 10,
  start: 0,
  order: 'desc',
  fields: ['message']
};

logger.query(options, function (err, results) {
  if (err) {
    throw err;
  }
  
  console.log(results);
});


winston.stream({ start: -1 }).on('log', function(log) {
  console.log(log);
});


const winston = require('winston');

winston.log('log', 'Hello distributed log files!');
winston.info('Hello again distributed logs');

winston.levle = 'debug';
winston.log('debug', 'Now my debug messages are written to console!');

const files = new winston.transports.file({ filename: 'combiled.log' });
const console = new winston.transports.Console();

winston.add(console);
winston.add(files);
winston.remove(console);


winston.configure({
  transports: [
    new winston.transports.File({ filename: 'somefile.log' })
  ]
});


const transport = new winston.transports.Console();
const logger = winston.createLogger({
  transports: [transport]
});

logger.on('finish', function (inof) {
});

logger.info('CHILL WINSTON!', { seriously: true });
logger.end();

logger.on('error', function (err) {
});

logger.emitErrs = false;


const winston = require('winston');
const { format } = winston;
const { combine, label, json } = format;

winston.loggers.add('category1', {
  format: combine(
    label({ label: 'category one' }),
    json()
  ),
  transports: [
    new winston.transports.Console({ level: 'silly' }),
    new winston.transports.File({ filename: 'somefile.log' })
  ]
});


winston.loggers.add('category2', {
  format: combine(
    label({ label: 'category two' }),
    json()
  ),
  transports: [
    new winston.transportsHttp({ host: 'localhost', port:8080 })
  ]
});


const winston = require('winston');

const category1 = winston.loggers.get('category1');
const category2 = winsotn.loggers.get('category2');

category1.info('loging to file and console transports');
category2.info('loging to http trasport'); 


const winston = require('winston');
const { format } = winston;
const { combine, json } = format;

const container = new winston.Container();

container.add('category1', {
  format: combine(
    label({ lable: 'category one' }),
    json()
  ),
  transports: [
    new winston.transports.Console({ level: 'silly' }),
    new winston.transports.File({ filename: 'somefile.log' })
  ]
});

const category1 = containter.get('category1');
category1.info('loggin to file and console transports');
```

```
npm install winston
yarn add winsotn
npm test
```

```
{
  emerg: 0,
  alert: 1,
  crit: 2,
  error: 3,
  warning: 4,
  notice: 5,
  info: 6,
  debug: 7
}

{
  error: 0,
  warn: 1,
  info: 2,
  verbose: 3,
  debug: 4,
  silly: 5
}

```
