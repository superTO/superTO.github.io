---
title: Typescript - Type Guard
date: 2021-10-18 23:32:39
tags: Typescript
categories: 
---
## 每次都要用as強制型別轉換?

```
enum Gender {
    MALE = 'male',
    FEMALE = 'female'
}

const foo = (gender = 'male' as Gender) => {
    return Object.values(Gender).includes(gender);
}
```

## Sol 1 Type Guard
```
enum Gender {
    MALE = 'male',
    FEMALE = 'female'
}

const isGender = (gender: any): gender is Gender => {
    return Object.values(Gender).includes(gender);
}

const foo = (gender = 'male') => {
    if(isGender(gender)) {
        // .includes(gender) // gender 的型別是Gender
        return Object.values(Gender).includes(gender);
    }
}
```

- 額外補充 「Narrowing」

## Sol 2 Generics
```
enum Gender {
    MALE = 'male',
    FEMALE = 'female'
}

enum Gender_2 {
    MALE = 'male',
    FEMALE = 'female'
}

const mapper = {
    [Gender_2.MALE]: Gender.MALE,
    [Gender_2.FEMALE]: Gender.FEMALE
}

const createMapper = <T>(mapping: T) => (value: keyof T | null): T[keyof T] | undefined => {
    return value === null ? undefined : mapping[value];
}

const foo = (gender: Gender_2.MALE) => {
    const data = { gender: Gender.MALE };
    const getMapper = createMapper(mapper);
    const trans = getMapper(gender);
    
    return trans === data.gender;
}
```

#### Reference

[Typescript 一些令人又愛又恨的內容 — Type Guard、Narrowing](https://medium.com/onedegree-tech-blog/typescript-%E4%B8%80%E4%BA%9B%E4%BB%A4%E4%BA%BA%E5%8F%88%E6%84%9B%E5%8F%88%E6%81%A8%E7%9A%84%E5%85%A7%E5%AE%B9-type-guard-narrowing-1655a9ae2a4d)