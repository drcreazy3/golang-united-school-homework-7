package coverage

import (
	"fmt"
	"os"
	"testing"
	"time"
	"reflect"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestLen(t *testing.T) {
	people := People{Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)}}
	
	tData := map[string]struct {
		P People
		Expected int
	}{
		"empty":          {P:People{}, Expected: 0},
		"some values":    {P:people, Expected: 1},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			actual := v.P.Len();
			if actual != v.Expected {
				t.Errorf("[%s] expected: %d, actual %d", name, v.Expected, actual)
			}
		})
	}

}

func TestLess(t *testing.T) {
	people := People{
		Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Obama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Abama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
		Person{firstName:"Aarak", lastName: "Abama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
	}
	
	tData := map[string]struct {
		P1 int
		P2 int
		Expected bool
	}{
		"diff birthdays p": {P1:0, P2:1, Expected:true},
		"diff birthdays n": {P1:1, P2:0, Expected:false},
		"same birthdays but different last name p": {P1:2, P2:1, Expected:true},
		"same birthdays but different last name n": {P1:1, P2:2, Expected:false},
		"same birthdays but different first name p": {P1:3, P2:2, Expected:true},
		"same birthdays but different first name n": {P1:2, P2:3, Expected:false},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			actual := people.Less(v.P1, v.P2)
			if actual != v.Expected {
				t.Errorf("[%s] expected: %t, actual %t", name, v.Expected, actual)
			}
		})
	}
}

func TestSwap(t *testing.T) {
	people := People{
		Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Obama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
	}


	tData := map[string]struct {
		P1 int
		P2 int
	}{
		"swap": {P1:0, P2:1},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			oldP1 := people[v.P1]
			oldP2 := people[v.P2]
			people.Swap(v.P1, v.P2)

			if oldP1 != people[v.P2] || oldP2 != people[v.P1]  {
				t.Errorf("Can not swipe items")
			}
		})
	}
}

//
func TestNew(t *testing.T) {
	tData := map[string]struct {
		M string
		E error
		Expected *Matrix
	}{
		"success": {M:"3 3 3\n3 3 3\n3 3 3", E:nil, Expected: &Matrix{rows: 3, cols: 3}},
		"mismatch row length": {M:"3 3 3\n3 3", E:fmt.Errorf("Rows need to be the same length"), Expected: nil},
		"character in row": {M:"3 3 3\n3 3 3\n3 A 3", E:fmt.Errorf("strconv.Atoi: parsing \"A\": invalid syntax"), Expected: nil},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			m, err := New(v.M);

     		if v.E != nil && (err.Error() != v.E.Error()) {
				t.Errorf("[%s] unexpected error returned: %s", name, err)
			}

			if m == nil && v.Expected == nil {
				return
			}

			if v.Expected.cols != m.cols || v.Expected.rows != m.rows {
				t.Errorf("[%s] exp/act rows or columns count mismatch (%d/%d), (%d/%d)", name, v.Expected.rows, m.rows, v.Expected.cols, m.cols)
			}
		})
	}
}

func TestRows(t *testing.T) {
	tData := map[string]struct {
		M string
		E [][]int
	}{
		"get rows": {M:"1 2 3\n1 2 3\n1 2 3", E:[][]int{{1,2,3}, {1,2,3},{1,2,3}}},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			m, _ := New(v.M);
			
			if !reflect.DeepEqual(m.Rows(), v.E) {
				t.Errorf("[%s] exp and actual rows differs", name)
			}
		})
	}
}

func TestCols(t *testing.T) {
	tData := map[string]struct {
		M string
		E [][]int
	}{
		"get cols": {M:"1 2 3\n1 2 3\n1 2 3", E:[][]int{{1,1,1}, {2,2,2},{3,3,3}}},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			m, _ := New(v.M);
			
			if !reflect.DeepEqual(m.Cols(), v.E) {
				t.Errorf("[%s] exp and actual cols differs", name)
			}
		})
	}
}

func TestSet(t *testing.T) {
	tData := map[string]struct {
		R int
		C int
		V int
		Expected bool
	}{
		"successful": {R: 0, C:0, V:12, Expected: true},
		"wrong row": {R: -1, C:0, V:12, Expected: false},
		"wrong row2": {R: 3, C:0, V:12, Expected: false},
		"wrong col": {R: 0, C:-1, V:12, Expected: false},
		"wrong col2": {R: 0, C:3, V:12, Expected: false},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			m, _ := New("1 2 3\n1 2 3\n1 2 3");
			set := m.Set(v.R, v.C, v.V)
			if set != v.Expected {
				t.Errorf("[%s] set action finished differently", name)
			}
			
			if set {
				rows := m.Rows()
				if rows[v.R][v.C] != v.V {
					t.Errorf("[%s] expected value %d in row %d col %d", name, v.V, v.R, v.C)
				}
			}
		})
	}
}