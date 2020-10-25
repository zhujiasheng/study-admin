<template>
  <div style="padding-top:20px;background:#fff;height:70vh;">
    <Form
      ref="formValidate"
      :model="formValidate"
      :rules="ruleValidate"
      :label-width="80"
      inline
    >
      <FormItem label="课程标题" prop="name">
        <Input v-model="formValidate.name" placeholder="请输入"></Input>
      </FormItem>
      <FormItem label="讲师" prop="mail">
        <Input v-model="formValidate.mail" placeholder="请输入"></Input>
      </FormItem>
      <FormItem label="状态" prop="mail">
        <Select v-model="model1">
          <Option
            v-for="item in statusList"
            :value="item.value"
            :key="item.value"
            >{{ item.label }}</Option
          >
        </Select>
      </FormItem>
      <Button type="primary" @click="handleSubmit('formValidate')">查询</Button>
      <Button @click="handleReset('formValidate')" style="margin-left: 8px"
        >重置</Button
      >
    </Form>
    <div style="margin-top:200px;">
      <Table border ref="selection" :columns="columns4" :data="data1"></Table>
      <Button @click="handleSelectAll(true)">Set all selected</Button>
      <Button @click="handleSelectAll(false)">Cancel all selected</Button>
    </div>
  </div>
</template>
<script>
import { getTableData } from "@/api/data";
export default {
  name: "desk-list",
  data() {
    return {
      columns4: [
        {
          type: "selection",
          width: 60,
          align: "center"
        },
        {
          title: "Name",
          key: "name"
        },
        {
          title: "Age",
          key: "age"
        },
        {
          title: "Address",
          key: "address"
        }
      ],
      data1: [
        {
          name: "John Brown",
          age: 18,
          address: "New York No. 1 Lake Park",
          date: "2016-10-03"
        }
      ],
      statusList: [
        {
          value: "1",
          label: "显示"
        },
        {
          value: "0",
          label: "下线"
        }
      ],
      formValidate: {
        name: "",
        mail: "",
        city: "",
        gender: "",
        interest: [],
        date: "",
        time: "",
        desc: ""
      },
      ruleValidate: {
        name: [
          {
            required: true,
            message: "不能为空",
            trigger: "blur"
          }
        ],
        mail: [
          {
            required: true,
            message: "不能为空",
            trigger: "blur"
          },
          { type: "email", message: "Incorrect email format", trigger: "blur" }
        ],
        city: [
          {
            required: true,
            message: "Please select the city",
            trigger: "change"
          }
        ],
        gender: [
          { required: true, message: "Please select gender", trigger: "change" }
        ],
        interest: [
          {
            required: true,
            type: "array",
            min: 1,
            message: "Choose at least one hobby",
            trigger: "change"
          },
          {
            type: "array",
            max: 2,
            message: "Choose two hobbies at best",
            trigger: "change"
          }
        ],
        date: [
          {
            required: true,
            type: "date",
            message: "Please select the date",
            trigger: "change"
          }
        ],
        time: [
          {
            required: true,
            type: "string",
            message: "Please select time",
            trigger: "change"
          }
        ],
        desc: [
          {
            required: true,
            message: "不能为空",
            trigger: "blur"
          },
          {
            type: "string",
            min: 20,
            message: "不能为空",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    handleSelectAll(status) {
      this.$refs.selection.selectAll(status);
    },
    handleSubmit(name) {
      this.$refs[name].validate(valid => {
        if (valid) {
          this.$Message.success("Success!");
        } else {
          this.$Message.error("Fail!");
        }
      });
    },
    handleReset(name) {
      this.$refs[name].resetFields();
    }
  },
  mounted() {
    getTableData().then(res => {
      console.log(res, "res");
      this.tableData = res.data;
    });
  }
};
</script>
