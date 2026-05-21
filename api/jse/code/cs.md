# CS

> `jse.code.CS`

**核心职能**：包含 jse 框架中所有编译期确定的不可变常量——版本号、原子数据键名与列索引、物理单位、元素周期表信息、正则表达式、零长度数组等。静态常量类，不实例化。标注 `@ApiStatus.Internal` 的内部字段已排除（`RANDOM_`, `SUC_FUTURE`, `ERR_FUTURE`, `ERR_FUTURES`, `EPT_STR_FUTURE`, `NUL_PRINT_STREAM`）。

```java
// jse 版本号
final static String VERSION            // "4.0.1"
final static int VERSION_NUMBER        // 4_00_01_00

// 全局随机数生成器
final static IRandom RANDOM
final static int MAX_SEED              // 最大随机种子值，900000000

// 零向量常量（只读），坐标全为 0
final static IXYZ XYZ_ZERO

// 数组切片通配符，表示保留全部维度
final static SliceType ALL

// Sleep/Timeout 常量（ms）
final static long INTERNAL_SLEEP_TIME       // 1
final static long SYNC_SLEEP_TIME           // 10
final static long SYNC_SLEEP_TIME_2         // 20
final static long FILE_SYSTEM_SLEEP_TIME    // 100
final static long FILE_SYSTEM_SLEEP_TIME_2  // 200
final static long SSH_SLEEP_TIME            // 500
final static long SSH_SLEEP_TIME_2          // 1000
final static long SYNC_TIMEOUT              // 500
final static long FILE_SYSTEM_TIMEOUT       // 10000

// ===== 原子数据键名常量（用于 Data/Dump 读写） =====
final static String[] ATOM_DATA_KEYS                    // ["x","y","z","id","type","vx","vy","vz"]
final static String[] ATOM_DATA_KEYS_VELOCITY           // ["vx","vy","vz"]
final static String[] ATOM_DATA_KEYS_BOND               // ["type","id1","id2"]
final static String[] ATOM_DATA_KEYS_XYZ                // ["x","y","z"]
final static String[] ATOM_DATA_KEYS_XYZID              // ["x","y","z","id"]
final static String[] ATOM_DATA_KEYS_TYPE_XYZ           // ["type","x","y","z"]
final static String[] ATOM_DATA_KEYS_ID_TYPE_XYZ        // ["id","type","x","y","z"]
final static String[] ATOM_DATA_KEYS_ID_TYPE_MOL_CHARGE_XYZ // ["id","type","mol","charge","x","y","z"]
final static String[] ALL_ATOM_DATA_KEYS                // ["id","type","x","y","z","vx","vy","vz"]
final static String[] STD_ATOM_DATA_KEYS                // == ATOM_DATA_KEYS_ID_TYPE_XYZ

// ===== 原子数据列索引常量 =====
// ATOM_DATA_KEYS 列索引
final static int DATA_X_COL, DATA_Y_COL, DATA_Z_COL     // 0,1,2
final static int DATA_ID_COL, DATA_TYPE_COL             // 3,4
final static int DATA_VX_COL, DATA_VY_COL, DATA_VZ_COL  // 5,6,7
// ATOM_DATA_KEYS_XYZ 列索引
final static int XYZ_X_COL, XYZ_Y_COL, XYZ_Z_COL        // 0,1,2
// ATOM_DATA_KEYS_XYZID 列索引
final static int XYZID_X_COL, XYZID_Y_COL, XYZID_Z_COL, XYZID_ID_COL // 0,1,2,3
// ATOM_DATA_KEYS_TYPE_XYZ 列索引
final static int TYPE_XYZ_TYPE_COL, TYPE_XYZ_X_COL, TYPE_XYZ_Y_COL, TYPE_XYZ_Z_COL // 0,1,2,3
// ALL_ATOM_DATA_KEYS 列索引
final static int ALL_ID_COL, ALL_TYPE_COL               // 0,1
final static int ALL_X_COL, ALL_Y_COL, ALL_Z_COL        // 2,3,4
final static int ALL_VX_COL, ALL_VY_COL, ALL_VZ_COL     // 5,6,7
// STD_ATOM_DATA_KEYS 列索引
final static int STD_ID_COL, STD_TYPE_COL               // 0,1
final static int STD_X_COL, STD_Y_COL, STD_Z_COL        // 2,3,4
// ATOM_DATA_KEYS_VELOCITY 列索引
final static int STD_VX_COL, STD_VY_COL, STD_VZ_COL     // 0,1,2
// ATOM_DATA_KEYS_BOND 列索引
final static int STD_BOND_TYPE_COL, STD_BOND_ID1_COL, STD_BOND_ID2_COL // 0,1,2
final static double R_NEAREST_MUL                       // 截断半径默认倍率 1.5

// ===== 零长度数组常量（避免频繁分配空数组） =====
final static OpenOption[] ZL_OO
final static String[] ZL_STR
final static Object[] ZL_OBJ
final static double[][] ZL_DOUBLE_BI
final static double[] ZL_DOUBLE
final static float[] ZL_FLOAT
final static int[] ZL_INT
final static long[] ZL_LONG
final static short[] ZL_SHORT
final static byte[] ZL_BYTE
final static boolean[] ZL_BOOL
final static Vector ZL_VEC
final static RowMatrix ZL_MAT

// ===== 正则表达式常量 =====
final static Pattern BLANKS_OR_EMPTY      // \s*
final static Pattern BLANKS               // \s+
final static Pattern COMMA                // \s*,\s*
final static Pattern COMMA_OR_BLANKS      // \s*[,\s]\s*
final static Pattern DOT                  // \.

// ===== 物理单位 =====
// `_` 前缀为基本物理常数，无前缀为单位换算因子；设计参考 ase.units
final static Map<String, Double> UNITS        // 2018 CODATA 版本
final static Map<String, Double> UNITS_ASE    // 2014 CODATA 版本（ASE 默认）
final static double K_B       // Boltzmann 常数, eV/K
final static double H_BAR     // Reduced Planck 常数, eV*ps
final static double N_A       // Avogadro 常数
final static double E_V       // Electron volt, g*Å²/ps² == 0.1J
final static double EV_TO_J   // eV 到 Joule 转换系数（= UNITS.get("_e")）
final static double EV_TO_KCAL// eV 到 kcal/mol 转换系数（= UNITS.get("mol") / UNITS.get("kcal")）

// ===== 元素周期表信息（118 种元素） =====
final static String[] SYMBOLS                     // ["H","He","Li",...]
final static List<String> ATOMIC_NUMBER_TO_SYMBOL // 原子序号→符号（1-based）
final static Map<String, Integer> SYMBOL_TO_ATOMIC_NUMBER // 符号→原子序号
final static Map<String, Double> MASS             // 原子质量
final static Map<String, Color> COLOR             // 可视化颜色（ovito 配色）
final static Map<String, Double> SIZE             // 可视化大小
```
