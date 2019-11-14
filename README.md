# chart-test

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run dev
```

### Compiles and minifies for production
```
npm run build
```

### Solution:
  Im using axios to get data from URL "http://www.mocky.io/v2/5dca723f33000073003ded0c", this give me data to setter in my object using chartjs to create chart. Im using map to setter data from object to show in chart, in this case: 'total_approved', 'total_disapproved'.
  
  When i setter data from endpoint, is neccesary to put data in 'chartdata', but i have a problem, im setter the labels, but in the object dont have names, but i have that in my email: '15 a 19 años', '20 29 años', '30-49 años', '50-64 años', 'Más de 65'. I need to push that labels.

  I see my 'chartdata' is a object, im used 'chardata.datasets' to fill that data, labels im push in the object. but i need to initialize 'null' my array of 'datasets', when i have the data, show them in 'DOM'.
  
  The swipe button is only interactive to show chart

