# Utils

### MAC地址/IP地址排序

```js
const columns = ref([
    ...,
    {
        title: 'MAC Address',
        dataIndex: 'address',
        key: 'address',
        width: 140,
        sorter: (a, b) => compareMac(a.address, b.address)
    },
    {
        title: 'Internal IP',
        dataIndex: 'local_ip',
        key: 'local_ip',
        width: 164,
        sorter: (a, b) => compareIp(a.local_ip, b.local_ip)
    }
])
 
// ip排序
/**
 *
 * @param {*} ip1
 * @param {*} ip2
 * @returns 该函数接受两个 IP 地址字符串作为参数，将它们转换为一个整数，通过分解每个八位字节并将其左移适当的位数（8 位）来实现。这样，整个 IP 地址就可以作为一个大整数进行比较
 * reduce：通过位运算（左移和加法）将四个八位字节合并成一个数
 */
const compareIp = (ip1, ip2) => {
  const ipToNumber = ip => {
    return ip.split('.').reduce((acc, octet) => (acc << 8) + Number(octet), 0)
  }
  return ipToNumber(ip1) - ipToNumber(ip2)
}
 
// mac排序
/**
 *
 * @param {*} mac1
 * @param {*} mac2
 * @returns 该函数接受两个 MAC 地址字符串作为参数，将它们以十六进制形式解析为整数，然后进行比较。我们通过 split(':').join('') 方法将 MAC 地址中的冒号去掉，
 * 得到一个长十六进制字符串，再用 parseInt 将其转换为整数
 */
const compareMac = (mac1, mac2) => {
  const macToNumber = mac => {
    return parseInt(mac.split(':').join(''), 16)
  }
  return macToNumber(mac1) - macToNumber(mac2)
}
```



### differ/clone

```js
import { transform, isEqual, isObject, cloneDeep } from 'lodash';

export function differ(base, obj) {
  return transform(base, function (result, value, key) {
    if (!isEqual(value, obj[key])) {
      result[key] = isObject(value) && isObject(obj[key]) ? differ(value, obj[key]) : value;
    }
  });
}

export const clone = cloneDeep;
```





































































