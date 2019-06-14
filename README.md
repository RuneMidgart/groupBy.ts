# groupBy.ts
TypeScript中的groupBy方法, 与C#中linq用法一致.  
The groupBy method in TypeScript, consistent with the usage of linq in C#.  
***
```ts
interface Group<TKey, TValue>
{
    key: TKey;
    values: TValue[];
}

Array.prototype.groupBy = function<TKey,TValue>(keyFn:(t:TValue)=>TKey):Group<TKey,TValue>[]{
    const result: Group<TKey, TValue>[] = [];
    const map = new Map<TKey, Group<TKey, TValue>>();
    this.forEach(t =>
    {
        const k = keyFn(t);
        if (map.has(k))
        {
            map.get(k)!.values.push(t);
        } else
        {
            const g = {
                key: k,
                values: [t],
            };
            map.set(k, g);
            result.push(g);
        }
    });
    return result;
}
```
确保上述代码被运行.  
Make sure the above code is picked up.  
***
```ts
interface Array<T>
{
  groupBy<TKey, TValue>(func: (x: TValue) => TKey): Group<TKey, TValue>[]
}
```
将这段代码添加到 *\*.d.ts* 文件.  
Add this code to the *\*.d.ts* file.  
