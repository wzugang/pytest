#include<python2.7/Python.h>

/*
#define Py_TYPE(o)    (((PyObject*)(o))->ob_type)
#define Py_REFCNT(o)  (((PyObject*)(o))->ob_refcnt)
#define Py_SIZE(o)    (((PyVarObject*)(o))->ob_size)

#define PyList_CheckExact(op) ((op)->ob_type == &PyList_Type)
return func->ob_type->tp_name;
#define PyList_CheckExact(op) (Py_TYPE(op) == &PyList_Type)
return Py_TYPE(func)->tp_name;
*/

/*  pytest.pytest(1,"aaaaaa","bbbbbb",a=1,b=2,c="cccccc")
    pytest.pytest(1,"aaa","bbb","abc") */
PyObject* pytest(PyObject* self, PyObject *args, PyObject *kwargs)
{
    int i = 0;
    char*p = NULL;
    char*pafter = NULL;
    PyObject* pObj = NULL;
    PyObject* iterator = NULL;
    PyObject *arg = NULL;
    char* ptemp = NULL;
    long ltemp = 0;
    int len = 0;

    (void)kwargs;
    /* i int */
    /* s string */
    /* | the after is optional */
    /* O the type is PyObject */
    if (!PyArg_ParseTuple(args, "is|sO", &i, &p, &pafter, &pObj))
    {
        return NULL;
    }
    printf("hello pytest i=%d, p=%s, ", i, p);

    if(pafter)
    {
        printf("pafter=%s, ", pafter);
    }

    if (pObj)
    {
        printf("object->");
        if(PyString_Check(pObj))
        {
            len = PyString_GET_SIZE(pObj);
            ptemp = PyString_AS_STRING(pObj);
            printf("str(%d)=%s, ", len, ptemp);
        }
        else if(PyInt_Check(arg)) /* PyObject can not be int */
        {
            ltemp = PyInt_AS_LONG(pObj);
            printf("long=%l, ", ltemp);
        }
        /*
        iterator = PyObject_GetIter(pObj);
        while ( (arg = PyIter_Next(iterator)))
        {
            printf("arg:");
            if (PyString_Check(arg))
            {
                len = PyString_GET_SIZE(arg);
                ptemp = PyString_AS_STRING(arg);
                printf("str(%d)=%s, ", len, ptemp);
            }
            else if (PyInt_Check(arg))
            {
                itemp = PyInt_AS_LONG(arg);
                printf("int=%d, ", itemp);
            }
            Py_DECREF(arg);
        }
        Py_DECREF(iterator);
        */
    }
    printf("\n");

    Py_RETURN_NONE;
}

static PyMethodDef pytestMethod[] = {
    {"pytest", (PyCFunction) pytest, METH_VARARGS | METH_KEYWORDS, "this is a py test."},
    {NULL,NULL,0,NULL}
};

PyMODINIT_FUNC initpytest(void)
{
    PyObject *module;
    PyObject *version_string;

    module = Py_InitModule("pytest", pytestMethod);

    if (module == NULL)
    {
        return;
    }

    version_string = PyString_FromString ("version-1.0");
    PyModule_AddObject(module, "__version__", version_string);
}
