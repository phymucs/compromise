```js
//greedy match issue
nlp(`wayne's world, party time`)
  .match('#Noun+? wayne')
  .debug()

nlp('Toronto Ontario foo')
  .match('(him|her|it|#Person|#Place|#Organization)+ .')
  .debug()
```

dangling child replace....

```js
let doc = nlp("springfield, springfield, it's a hell of a town.")
// keep a 'dangling' child document
let a = doc.match('a hell of a town')
// transform the parent document
doc.replace('hell of a', 'reasonable')
//dangling document is updated?
return a.text()
```

empty split() parent

```js
let doc = nlp(`i have two questions for Homer - 'Why lie?' and 'Lies, why?'`)
doc
  .quotations()
  .split()
  .out('array')
doc.clauses().split()
```

ngram collisions

```js
let doc = nlp('he fished and caught two fish')
doc.normalize('heavy')
console.log(doc.ngram())
```

syllables issues

```js
let doc = nlp(`Andreas Johnsson, Auston Matthews, and Zach Hyman.`)
let names = doc.clauses().split()
let json = names.syllables()
```

possessive, sentence period

```js
nlp(`Wayne's World, party-time, excellent!! `).text('reduced')
nlp(`Wayne's World, party-time, excellent!! `).text('root')
```

```js
var doc = nlp('we get it, you vape.')
doc.verbs().toNegative()
console.log(doc.text())
```

```js
let nlpA = nlp.clone()
nlp.extend(require('compromise-dates'))
return {
  before: nlpA('quarter to nine').json(),
  after: nlp('quarter to nine').json(),
}
```

```js
console.log(doc.normalize('heavy').text())
```

```js
let doc = nlp('I’m lookin’ for Amanda').debug()
```

did/would contractions

```js
let doc = nlp(`what’d be good`).debug()
```

text-replace

```js
let doc = nlp('i worked at the F.B.I')
doc = doc.match('(#Acronym|#Abbreviation)').replaceWith(d => {
  return d
})
doc.debug()
```

### Jan 5

```js
nlp('  we like Roy!    we like Roy!!  ')
  .trim()
  .text()
```

```js
nlp(`why can't i have no kids and three money?`)
  .contractions()
  .expand()
  .text()
```

```js
nlp('Garth, I’m going to be frank.')
  .verbs()
  .toFutureTense()
  .all()
  .text()

nlp('WE’RE NOT WORTHY! WE’RE NOT WORTHY!')
  .verbs()
  .toFutureTense()
  .all()
  .text()

nlp('All my life I’ve had one dream, to accomplish my many goals.')
  .verbs()
  .toGerund()
  .all()
  .text()

nlp(`powerful like a gorilla, yet soft and yielding like a nerf ball`)
  .nouns()
  .toPlural()
  .all()
  .text()

nlp(`I'm not going to jail for you, or ANYBODY.`)
  .nouns()
  .toPlural()
  .all()
  .text()

nlp(`hey pal, did you get a load of the nerd?`)
  .nouns()
  .toPlural()
  .all()
  .text()
```

### Jan 15

match cached numbers?

```js
nlp('four').match('4')
```

### Jan 21

```js
let doc = nlp('pack a lunch for sam sunday morning')
```

### Jan 23

```js
let arr = [
  // *explicit-dates**,
  // `march 2nd`,
  // `2 march`,
  // `tues march 2`,
  `march the second`,
  // `on the 2nd`,
  // // *numerical-dates**,
  // `1999/03/02`,
  // `1999-03-02`,
  // `03-02-1999`,
  // `03/02`,
  // `2015.08.13`,
  // // *named-dates**,
  // `today`,
  // `easter`,
  // `q1`,
  // `tomorrow`,
  // // *time:**,
  // `2pm`,
  // `2:12pm`,
  // `2:12`,
  // `02:12:00`,
  // `2 oclock`,
  // `before 1`,
  // `noon`,
  // `at night`,
  // `in the morning`,
  // `tomorrow evening`,
  // // *timezone:**,
  // `eastern time`,
  // `est`,
  // `peru time`,
  // `GMT+9`,
  // // *relative duration**,
  // `this march`,
  // `this week`,
  // `this sunday`,
  // `next april`,
  // `this past year`,
  // `second week of march`,
  // `last weekend of march`,
  // `last spring`,
  // `the saturday after next`,
  // // *punt**,
  // `two days after tomorrow`,
  // `in seven weeks`,
  // `2 weeks from now`,
  // `2 weeks after`,
  // `2 years 4 months 5 days ago`,
  // `a week friday`,
  // `a week and a half before`,
  // `on the 1st`,
  // // *start/end**,
  // `end of the week`,
  // `start of next year`,
  // `start of next year`,
  // `middle of q2 last year`,
]

// let json = doc.dates({}).json()
// console.log(json)
```

### lookup duplicates
```js
let doc = nlp('spencer kelly is working here')
let res = doc.lookup(['spencer kelly', 'spencer'])
```