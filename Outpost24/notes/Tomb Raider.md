Our hero is in trouble and he needs your help!
Help him collect all the rare artifacts and unlock the secret.
But beware, danger lurks around every corner...

In the JavaScript we find this snippet:
```javascript
const _0x2f8a = [
        '4p7l1', 'p07R3', 'S2x9Q', 'apply', 'qopI5',
        'ufn23', 'n465l', 'charAt', 'fromCharCode', 'length'
    ];
    
    function _0x19fe(s, k) {
        let a = '';
        for(let i = 0; i < s.length; i++) {
            let c = s.charCodeAt(i);
            if (c >= 65 && c <= 90) a += String.fromCharCode(((c - 65 + k) % 26) + 65);
            else if (c >= 97 && c <= 122) a += String.fromCharCode(((c - 97 + k) % 26) + 97);
            else a += s.charAt(i);
        }
        return a;
    }
    
    const _p1 = [79, 50, 52];
    const _p2 = [123, 49, 77, 95];
    const _p3 = [72, 52, 87, 33];
    const _p4 = [78, 54, 95, 70];
    const _p5 = [85, 78, 78, 52, 65, 65, 82, 71, 52, 125];
    
    function getDecodedFlag() {
        if (obtainedItems.length === 5) {
            return [..._p1, ..._p2, ..._p3, ..._p4, ..._p5]
                .map(code => String.fromCharCode(code))
                .join('');
        }
        
        let result = '';
        const allParts = [_p1, _p2, _p3, _p4, _p5];
        const charsPerPart = flagTextLength / 5;
        
        for (let i = 0; i < 5; i++) {
            if (obtainedItems.includes(i)) {
                result += allParts[i].map(code => String.fromCharCode(code)).join('');
            } else {
                result += '•'.repeat(allParts[i].length);
            }
        }
        
        return result;
    }
    
    const flagTextLength = _p1.length + _p2.length + _p3.length + _p4.length + _p5.length;
```


By running saving and running the code in Node like this we get the flag.  
```javascript
const obtainedItems = [1,2,3,4,5]

const _p1 = [79, 50, 52];
const _p2 = [123, 49, 77, 95];
const _p3 = [72, 52, 87, 33];
const _p4 = [78, 54, 95, 70];
const _p5 = [85, 78, 78, 52, 65, 65, 82, 71, 52, 125];

function getDecodedFlag() {
	if (obtainedItems.length === 5) {
		return [..._p1, ..._p2, ..._p3, ..._p4, ..._p5]
		.map(code => String.fromCharCode(code))
		.join('');
}

let result = '';
const allParts = [_p1, _p2, _p3, _p4, _p5];
const charsPerPart = flagTextLength / 5;

for (let i = 0; i < 5; i++) {
	if (obtainedItems.includes(i)) {
		result += allParts[i].map(code => String.fromCharCode(code)).join('');

	} else {
		result += '•'.repeat(allParts[i].length);
	}
}

return result;
}

const flagTextLength = _p1.length + _p2.length + _p3.length + _p4.length + _p5.length;

console.log(getDecodedFlag())
```

```
strombach㉿pentest-vm)-[~]
└─$ node index.js 
O24{1M_H4W!N6_FUNN4AARG4}
```
