# Промисификация fs

## Releases

### Pre-Release

Ты уже работал с модулем `fs`, однако ты делал это через `callbacks` либо сихронные методы. Синхронные методы в случае работы с внешними хранилищами - не лучшая идея, а работа с коллбэками порой неудобна, да и выглядит страшновато, если они вкладываются друг в друга. К счастью у нас есть `Promises`! А это значит, что ты можешь обернуть асинхронные методы (те, что с `callbacks`) в промисы, и тогда работать с ними будет удобнее. Задание необходимо, чтобы ты разобрался в том, как работают промисы и как писать свои функции, возвращающие промисы.

> В задании нельзя использовать методы с окончанием `Sync` и методы из `fs.promises`.

Пример функции, оборачивающей асинхронную функцию (`setTimeout`) в `Promise`:
```js
function slowLog(seconds) {
  return new Promise((resolve, reject) => {
    if (typeof seconds === 'number') {
    console.log('Start: ', new Date());
    setTimeout(() => {
      console.log('End: ', new Date());
      resolve(`Ура! Прошло ${seconds} секунд`);
    }, seconds * 1000);
    } else {
      reject('Ошибка! Передайте аргумент типа Number!')
    }
  });
}

slowLog(5)
  .then(result => console.log(`***${result}***`))
  .catch(err => console.log(err));

// console:
// Start:  2020-02-14T13:50:30.600Z
// End:  2020-02-14T13:50:35.611Z
// ***Ура! Прошло 5 секунд***
```

## Release 0:

Теперь твоей задачей будет написать свои методы работы с `fs` с использованием `Promise`.
Начни с `fs.readFile()`! Напиши новую функцию, она будет возвращать `Promise`, статус которого становится `resolved`, когда файл прочитан. Далее промисифицируй остальные функции: `fs.readdir`, `fs.stat`, `fs.rename`.

## Release 1:

Теперь, используя промисы, напиши скрипт который приведет названия файлов в папке notes к формату `note-<Рандомная строка из 5 символов>-<Размер файла>-<Дата создания>.txt`.
Ты должен создать цепочку промисов используя ранее созданные промисифицированные функции. Добейся того, чтобы не было лишней вложенности колбэков.

