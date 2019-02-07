#### Solution

```java
class Person {
    int birth;
    int death;

    Person(int birth, int death) {
        this.birth = birth;
        this.death = death;
    }
}
```

```java
int maxAlive(Person[] people, int min, int max) {
    int[] populationDeltas = getDeltas(people, min, max);
    int maxAliveYear = findMaxAliveYear(populationDeltas);
    return maxAliveYear + min;
}

private int[] getDeltas(Person[] people, int min, int max) {
    int[] deltas = new int[max - min + 2];
    for (Person person : people) {
        deltas[person.birth - min]++;
        deltas[person.death + 1 - min]--; // We consider him/her alive on death year
    }
    return deltas;
}

private int findMaxAliveYear(int[] deltas) {
    int alive = 0;
    int maxAlive = 0;
    int maxYear = 0;
    for (int i = 0; i < deltas.length; i++) {
        alive += deltas[i];
        if (alive > maxAlive) {
            maxAlive = alive;
            maxYear = i;
        }
    }
    return maxYear;
}
```
