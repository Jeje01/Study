# 11일차 (22.02.02)
더러운 코드 고치기

## AS-IS
```javascript
const merry = document.querySelector(".js-clock");

function getClock() {
const christmas = new Date("2021, 12, 25");
const date = new Date();
const timeGap = christmas - date;

const xDay = Math.floor(timeGap / (1000 * 60 * 60 * 24));
const xHours = Math.floor(
(timeGap - xDay * 1000 * 60 * 60 * 24) / (1000 * 60 * 60)
);
const xMinutes = Math.floor((timeGap % (60 * 60 * 1000)) / (60 * 1000));
const xSeconds = Math.floor((timeGap % (60 * 1000)) / 1000);

const day = String(xDay).padStart(2, "0");
const hours = String(xHours).padStart(2, "0");
const minutes = String(xMinutes).padStart(2, "0");
const seconds = String(xSeconds).padStart(2, "0");

merry.innerText = `${day}d ${hours}h ${minutes}m ${seconds}s`;
}

getClock();
setInterval(getClock, 1000);
```

## TO-BE
```javascript
const merryChristmas = document.querySelector(".js-clock");

const TOTAL_MILLISECONDS_OF_ONE_SECOND = 1000
const TOTAL_MILLISECONDS_OF_ONE_MINUTE = TOTAL_MILLISECONDS_OF_ONE_SECOND * 60
const TOTAL_MILLISECONDS_OF_ONE_HOUR = TOTAL_MILLISECONDS_OF_ONE_MINUTE * 60
const TOTAL_MILLISECONDS_OF_ONE_DAY = TOTAL_MILLISECONDS_OF_ONE_HOUR * 24

function getTimeUntilChristmas() {
  const christmas = new Date("2021, 12, 25");
  const now = new Date();
  const millisecondsUntilChristmas = christmas - now;

  const convertedTime = convertMillisecondsToTime(millisecondsUntilChristmas);

  merryChristmas.innerText = convertedTime;
}

function convertMillisecondsToTime(milliseconds) {
  const xDay = Math.floor(
    millisecondsUntilChristmas / TOTAL_MILLISECONDS_OF_ONE_DAY
  );
  const xHours = Math.floor(
    (millisecondsUntilChristmas - xDay * TOTAL_MILLISECONDS_OF_ONE_DAY) / TOTAL_MILLISECONDS_OF_ONE_HOUR
  );
  const xMinutes = Math.floor(
    (millisecondsUntilChristmas % TOTAL_MILLISECONDS_OF_ONE_HOUR) / TOTAL_MILLISECONDS_OF_ONE_MINUTE
  );
  const xSeconds = Math.floor(
    (millisecondsUntilChristmas % TOTAL_MILLISECONDS_OF_ONE_MINUTE) / TOTAL_MILLISECONDS_OF_ONE_SECOND
  );

  const day = addPadding(xDay);
  const hours = addPadding(xHours);
  const minutes = addPadding(xMinutes);
  const seconds = addPadding(xSeconds);

  return `${day}d ${hours}h ${minutes}m ${seconds}s`;
}

function addPadding(number) {
  return String(number).padStart(2, "0");
}

getTimeUntilChristmas();
setInterval(getTimeUntilChristmas, 1000);
```

## 수정사항
1. 의미를 해석해야하는 숫자를 상수로 교체
2. 함수를 고차원에서 저차원 순서로 분리
3. 중복되는 코드 함수로 분리
4. 길어지더라도 구체적인 의미를 담고 있는 변수명으로 수정
