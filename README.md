# Unity Project

### Coding
[ตามนี้เลย](https://unity.com/how-to/naming-and-code-style-tips-c-scripting-unity)

- พวกชื่อ Namespace, Class, Struct, Property, Function, Enum เป็นแบบ `PascalCase` หมด
- Serialzable Field เป็นแบบ `camelCase` เพราะใน Unity เวลาเราจะทำให้ตัวแปรมัน Serialize ได้ ต้องทำเป็น public field (ไม่ก็ใช้ [SerializeField] attribute) ทำแบบนี้เพื่อให้ชื่อตัวแปรมันไม่ซ้ำกับพวก Property 
- พวก Local Variable/Parameter เป็นแบบ `camelCase` หมด
- พวก Private/Protected Field ให้มี Prefix เป็น `_` ตามด้วยชื่อเป็นแบบ `camelCase` เช่น `_currentHp` 
- พวกชื่อตัวแปร Boolean ทำให้มันสื่อความหมายโดยใส่คำนำหน้าว่า Is, Has, Can อะไรงี้ เช่น `IsAlive`, `_hasArmor`, `CanUseSkill()`
- พวกชื่อ `delegate` ให้ใส่ Suffix ว่า `EventHandler` เช่น `public delegate void HpChangedEventHandler(int currentHp);`

ตัวอย่าง

```
namespace Company.GameName.Gameplay
{
    public delegate void HpChangedEventHandler(int currentHp);
    public class Character
    {
        private static int _allCharacterDeadCount = 0;
        public static int AllCharacterDeadCount => _allCharacterDeadCount;

        public float DamageAbsorbing = 0.5f;
        public int MaxHp = 100;
        public HpChangedEventHandler OnHpChanged;
        
        private int _currentHp;
        public string CurrentHp
        {
            get => _currentHp;
            set {
                if (_currentHp == value)
                    return;
                _currentHp = value;
                NotifyHpChanged(value);
                if (IsDead)
                    _allCharacterDeadCount++;
            }
        }

        public bool IsDead => _currentHp <= 0;

        private void NotifyHpChanged(int changedHp)
        {
            OnHpChanged?.Invoke(changedHp);
        }

        public void Revive()
        {
            if (IsDead)
                return;
            CurrentHp = MaxHp;
        }

        public void ApplyDamage(float damage)
        {
            int calculatedDamage = (int)(damage - (damage * DamageAbsorbing));
            CurrentHp -= calculatedDamage;
        }
    }
}
```

### Asset
[ตามนี้ไปก่อน](https://github.com/justinwasilenko/Unity-Style-Guide)
