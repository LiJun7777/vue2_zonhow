<template>
	<div class="formbuilder">
		<el-form
			:model="informationForm"
			:rules="rules"
			ref="informationForm"
			hide-required-asterisk
			label-position="top"
			size="mini"
		>
			<div class="left-basic">
				<div
					style="
						padding: 30px;
						display: flex;
						justify-content: space-between;
					"
				>
					<h1 style="font-size: 32px">个人信息登记表</h1>
					<div class="smallTitle" style="font-weight: 600">
						<p>ZONHOW</p>
						<p>中豪建设</p>
					</div>
				</div>
				<el-row :gutter="20">
					<el-col :span="8">
						<div>
							<div class="avatar">
								<img
									v-show="imageUrl"
									:src="imageUrl"
									style="width: 100%; height: 100%"
								/>
							</div>

							<el-upload
								ref="upload"
								action=""
								list-type="picture-card"
								:show-file-list="false"
								:auto-upload="false"
								:on-change="uploadImage"
								:before-upload="beforeAvatarUpload"
							>
								<el-button size="mini">上传</el-button>
							</el-upload>
						</div>
					</el-col>
					<el-col :span="16">
						<h4 class="title">一 基本信息</h4>
						<el-row :gutter="20">
							<el-col :span="12">
								<el-form-item label="姓名" prop="name">
									<el-input
										v-model.trim="informationForm.name"
									></el-input>
								</el-form-item>
								<el-form-item label="出生年月" prop="birthTime">
									<el-date-picker
										v-model="informationForm.birthTime"
										type="date"
										placeholder="出生年月"
										style="width: 100%"
									>
									</el-date-picker>
								</el-form-item>
							</el-col>
							<el-col :span="12">
								<el-form-item label="性别" prop="sex">
									<el-radio-group
										v-model="informationForm.sex"
									>
										<el-radio label="男"></el-radio>
										<el-radio label="女"></el-radio>
									</el-radio-group>
								</el-form-item>
								<el-form-item label="民族">
									<el-input
										v-model.trim="
											informationForm.typeEthnic
										"
									></el-input>
								</el-form-item>
							</el-col>
						</el-row>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="8">
						<el-form-item label="政治面貌" prop="typePolitical">
							<el-select
								v-model="informationForm.typePolitical"
								placeholder="请选择"
							>
								<el-option label="群众" :value="1"></el-option>
								<el-option
									label="中共党员"
									:value="2"
								></el-option>
							</el-select>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="身份证号" prop="identityNo">
							<el-input
								v-model.trim="informationForm.identityNo"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="社保号" prop="socialNo">
							<el-input
								v-model.trim="informationForm.socialNo"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="8">
						<el-form-item label="手机" prop="phone">
							<el-input
								v-model.trim="informationForm.phone"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="电子邮件">
							<el-input
								v-model.trim="informationForm.email"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="固定电话">
							<el-input
								v-model.trim="informationForm.tel"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="8">
						<el-form-item label="开户行名称">
							<el-input
								v-model.trim="informationForm.bankname"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="16">
						<el-form-item label="银行卡号">
							<el-input
								v-model.trim="informationForm.account"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="16">
						<el-form-item label="联系地址">
							<el-input
								v-model.trim="informationForm.address"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="婚姻" prop="stateMarriage">
							<el-select
								v-model="informationForm.stateMarriage"
								placeholder="请选择"
							>
								<el-option label="否" :value="0"></el-option>
								<el-option label="是" :value="1"></el-option>
							</el-select>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="16">
						<el-form-item label="籍贯" prop="nativePlace">
							<el-input
								v-model.trim="informationForm.nativePlace"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="邮编">
							<el-input
								v-model.trim="informationForm.postcode"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="16">
						<el-form-item label="户口">
							<el-input
								v-model.trim="informationForm.identityAddress"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="8">
						<el-form-item label="血型">
							<el-input
								v-model.trim="informationForm.typeBlood"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
			</div>
			<div style="border: 1px solid gray; margin: 70px 0"></div>
			<div class="right-other" :class="pagefix" ref="rightOther">
				<h4 class="title">二 学业与技能信息</h4>
				<el-row :gutter="20">
					<el-col :span="6">
						<el-form-item label="毕业院校">
							<el-input
								v-model.trim="informationForm.graduatedSchool"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="6">
						<el-form-item label="学历" prop="education">
							<el-input
								v-model.trim="informationForm.education"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="6">
						<el-form-item label="专业">
							<el-input
								v-model.trim="informationForm.profession"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="6">
						<el-form-item label="职称">
							<el-input
								v-model.trim="informationForm.jobTitle"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="20">
					<el-col :span="6">
						<el-form-item label="外语水平">
							<el-input
								v-model.trim="
									informationForm.foreignLanguageLevel
								"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="6">
						<el-form-item label="计算机水平">
							<el-input
								v-model.trim="
									informationForm.computerSkillLevel
								"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="12">
						<el-form-item label="特长">
							<el-input
								v-model.trim="informationForm.specialty"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>

				<h4 class="title">三 面试信息</h4>
				<el-row :gutter="20">
					<el-col :span="6">
						<el-form-item
							label="面试部门"
							prop="interviewDepartment"
						>
							<el-input
								v-model.trim="
									informationForm.interviewDepartment
								"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="6">
						<el-form-item label="面试岗位" prop="interviewJob">
							<el-input
								v-model.trim="informationForm.interviewJob"
							></el-input>
						</el-form-item>
					</el-col>
					<el-col :span="12">
						<el-form-item label="报道时间">
							<el-input
								v-model.trim="informationForm.dateWork"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>

				<h4 class="title">四 紧急联系人</h4>
				<el-row style="margin-bottom: 10px">
					<el-table
						:data="informationForm.hrStaffInformationContactList"
						class="fourTable inputClass"
						style="width: 100%"
						border
					>
						<el-table-column label="联系人" width="175">
							<template slot-scope="scope">
								<el-form-item>
									<el-input
										v-model="scope.row.name"
									></el-input>
								</el-form-item>
							</template>
						</el-table-column>
						<el-table-column label="与本人关系" width="175">
							<template slot-scope="scope">
								<el-form-item>
									<el-input
										v-model="scope.row.name"
									></el-input>
								</el-form-item>
							</template>
						</el-table-column>
						<el-table-column label="联系方式" width="175">
							<template slot-scope="scope">
								<el-form-item>
									<el-input
										v-model="scope.row.name"
									></el-input>
								</el-form-item>
							</template>
						</el-table-column>
						<el-table-column label="操作" align="center">
							<template slot-scope="scope">
								<el-button
									v-if="
										isDelete(
											informationForm
												.hrStaffInformationContactList
												.length,
											scope.$index
										)
									"
									size="mini"
									type="text"
									@click="
										handleDelete(
											scope.$index,
											informationForm.hrStaffInformationContactList
										)
									"
									>删除</el-button
								>
								<el-button
									v-else
									size="mini"
									type="text"
									@click="
										handleAdd(
											scope.$index,
											informationForm.hrStaffInformationContactList
										)
									"
									>新增</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</el-row>

				<h4 class="title">五 工作经历</h4>
				<el-row style="margin-bottom: 10px">
					<el-table
						:data="informationForm.hrStaffInformationExperienceList"
						style="width: 100%"
						border
					>
						<el-table-column label="工作时间" width="100">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="工作单位" width="100">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="部门" width="80">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="职务" width="80">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="工作内容" width="170">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作" align="center">
							<template slot-scope="scope">
								<el-button
									v-if="
										isDelete(
											informationForm
												.hrStaffInformationExperienceList
												.length,
											scope.$index
										)
									"
									size="mini"
									type="text"
									@click="
										handleDelete(
											scope.$index,
											informationForm.hrStaffInformationExperienceList
										)
									"
									>删除</el-button
								>
								<el-button
									v-else
									size="mini"
									type="text"
									@click="
										handleAdd(
											scope.$index,
											informationForm.hrStaffInformationExperienceList
										)
									"
									>新增</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</el-row>

				<h4 class="title">六 家庭状况</h4>
				<el-row style="margin-bottom: 10px">
					<el-table
						:data="informationForm.hrStaffInformationFamilyList"
						style="width: 100%"
						border
					>
						<el-table-column label="关系" width="80">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="姓名" width="80">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="联系方式" width="100">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="工作单位" width="100">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="家庭地址" width="170">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作" align="center">
							<template slot-scope="scope">
								<el-button
									v-if="
										isDelete(
											informationForm
												.hrStaffInformationFamilyList
												.length,
											scope.$index
										)
									"
									size="mini"
									type="text"
									@click="
										handleDelete(
											scope.$index,
											informationForm.hrStaffInformationFamilyList
										)
									"
									>删除</el-button
								>
								<el-button
									v-else
									size="mini"
									type="text"
									@click="
										handleAdd(
											scope.$index,
											informationForm.hrStaffInformationFamilyList
										)
									"
									>新增</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</el-row>

				<h4 class="title">七 所获证书</h4>
				<el-row style="margin-bottom: 10px">
					<el-table
						:data="
							informationForm.hrStaffInformationCertificateList
						"
						style="width: 100%"
						border
					>
						<el-table-column label="证书名称" width="90">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="证书编号" width="90">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="发证时间" width="90">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="生效时间" width="90">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="持证人" width="90">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作" align="center">
							<template slot-scope="scope">
								<template
									v-if="
										isPreview(
											informationForm
												.hrStaffInformationCertificateList
												.length,
											scope.$index
										)
									"
								>
									<el-button
										size="mini"
										type="text"
										@click="
											handlePreview(
												scope.$index,
												informationForm.hrStaffInformationCertificateList
											)
										"
										>预览</el-button
									>
									<el-button
										size="mini"
										type="text"
										@click="
											handleDownload(
												scope.$index,
												informationForm.hrStaffInformationCertificateList
											)
										"
										>下载</el-button
									>
								</template>

								<el-button
									size="mini"
									type="text"
									v-if="
										isDelete(
											informationForm
												.hrStaffInformationCertificateList
												.length,
											scope.$index
										)
									"
									@click="
										handleDelete(
											scope.$index,
											informationForm.hrStaffInformationCertificateList
										)
									"
									>删除</el-button
								>

								<el-button
									v-else
									size="mini"
									type="text"
									@click="
										handleAdd(
											scope.$index,
											informationForm.hrStaffInformationCertificateList
										)
									"
									>新增</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</el-row>
				<h4 class="title">八 添加附件</h4>
				<el-row style="margin-bottom: 10px">
					<el-table
						:data="
							informationForm.hrStaffInformationCertificateList
						"
						style="width: 100%"
						border
					>
						<el-table-column label="附件名称" width="160">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="上传人" width="140">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="上传时间" width="150">
							<template slot-scope="scope">
								<span style="margin-left: 10px">{{
									scope.row.date
								}}</span>
							</template>
						</el-table-column>
						<el-table-column label="操作" align="center">
							<template slot-scope="scope">
								<template
									v-if="
										isPreview(
											informationForm
												.hrStaffInformationCertificateList
												.length,
											scope.$index
										)
									"
								>
									<el-button
										size="mini"
										type="text"
										@click="
											handlePreview(
												scope.$index,
												informationForm.hrStaffInformationCertificateList
											)
										"
										>预览</el-button
									>
									<el-button
										size="mini"
										type="text"
										@click="
											handleDownload(
												scope.$index,
												informationForm.hrStaffInformationCertificateList
											)
										"
										>下载</el-button
									>
								</template>

								<el-button
									size="mini"
									type="text"
									v-if="
										isDelete(
											informationForm
												.hrStaffInformationCertificateList
												.length,
											scope.$index
										)
									"
									@click="
										handleDelete(
											scope.$index,
											informationForm.hrStaffInformationCertificateList
										)
									"
									>删除</el-button
								>

								<el-button
									v-else
									size="mini"
									type="text"
									@click="
										handleAdd(
											scope.$index,
											informationForm.hrStaffInformationCertificateList
										)
									"
									>新增</el-button
								>
							</template>
						</el-table-column>
					</el-table>
				</el-row>
				<h4 class="title">九 其他</h4>
				<el-row :gutter="10" style="margin-bottom: 10px">
					<el-col :span="12">
						<el-form-item label="1.奖惩情况">
							<el-input
								v-model.trim="
									informationForm.interviewDepartment
								"
								type="textarea"
								resize="none"
								:rows="4"
							>
							</el-input>
						</el-form-item>
					</el-col>
					<el-col :span="12">
						<el-form-item label="2.个人学习计划">
							<el-input
								v-model.trim="informationForm.interviewJob"
								type="textarea"
								resize="none"
								:rows="4"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-row :gutter="10">
					<el-col :span="12">
						<el-form-item label="3.培训情况">
							<el-input
								v-model.trim="
									informationForm.interviewDepartment
								"
								type="textarea"
								resize="none"
								:rows="4"
							>
							</el-input>
						</el-form-item>
					</el-col>
					<el-col :span="12">
						<el-form-item label="4.备注">
							<el-input
								v-model.trim="informationForm.interviewJob"
								type="textarea"
								resize="none"
								:rows="4"
							></el-input>
						</el-form-item>
					</el-col>
				</el-row>
				<el-form-item>
					<el-button
						type="primary"
						@click="submitForm('informationForm')"
						>提交</el-button
					>
					<el-button @click="resetForm('informationForm')"
						>重置</el-button
					>
					<!-- <el-backtop
						target=".right-other"
						@click="resetForm('informationForm')"
					>
						<el-button>重置</el-button>
					</el-backtop> -->
				</el-form-item>
			</div>
		</el-form>
	</div>
</template>
<script>
export default {
	name: "InfoList",
	data() {
		var validatorPhone = function (rule, value, callback) {
			if (value === "") {
				callback(new Error("手机号不能为空"));
			} else if (!/^1\d{10}$/.test(value)) {
				callback(new Error("手机号格式错误"));
			} else {
				callback();
			}
		};
		return {
			timeid: null,
			pagefix: {
				"page-fix": false,
			},
			imageUrl: "",
			informationForm: {
				name: "", //姓名
				sex: "", //性别：1男2女
				birthTime: "", //出生日期
				identityNo: "", //证件号
				nativePlace: "", //籍贯
				typeEthnic: "", //民族
				typePolitical: "", //政治面貌 1群众2中共党员
				phone: "", //联系电话
				tel: "", //办公电话
				email: "", //email
				socialNo: "", //社保号
				stateMarriage: "", //婚姻状况 0否1是
				bankname: "", //开户行名称
				account: "", //账号
				photo: "", //照片
				address: "", //当前地址
				typeBlood: "", //血型
				identityAddress: "", //户口地址
				postcode: "", //邮编
				education: "", //学历
				graduatedSchool: "", //毕业院校
				profession: "", //专业
				jobTitle: "", //职称
				foreignLanguageLevel: "", //外语水平
				computerSkillLevel: "", //计算机水平
				specialty: "", //特长
				interviewDepartment: "", //面试部门
				interviewJob: "", //面试岗位
				dateWork: "", //报到时间
				memo: "", //备注
				rewardsAndPunishments: "", //奖惩情况
				studyPlan: "", //学习计划
				training: "", //培训情况
				interviewId: "", //面试ID
				hrStaffInformationCertificateList: [
					{
						//证明
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						no: "", //证书编号
						userName: "", //持证人
						certificateTypeId: "", //证书名称ID
						certificateTypeName: "", //证书名称
						dateIssue: "", //发证日期
						dateEffective: "", //生效日期
					},
					{
						//证明
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						no: "", //证书编号
						userName: "", //持证人
						certificateTypeId: "", //证书名称ID
						certificateTypeName: "", //证书名称
						dateIssue: "", //发证日期
						dateEffective: "", //生效日期
					},
				],
				hrStaffInformationContactList: [
					{
						//联系
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						name: "", //联系人姓名
						relationship: "", //与本人关系
						phone: "", //联系方式
					},
					{
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						name: "", //联系人姓名
						relationship: "", //与本人关系
						phone: "", //联系方式
					},
				],
				hrStaffInformationFamilyList: [
					{
						//家人
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						name: "", //姓名
						relationship: "", //关系
						phone: "", //联系方式
						companyName: "", //工作单位
						address: "", //家庭地址
					},
					{
						//家人
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						name: "", //姓名
						relationship: "", //关系
						phone: "", //联系方式
						companyName: "", //工作单位
						address: "", //家庭地址
					},
				],
				hrStaffInformationExperienceList: [
					{
						//经历
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						workDate: "", //工作时间
						companyName: "", //工作单位
						department: "", //部门
						job: "", //职务
						content: "", //工作内容
					},
					{
						//经历
						id: "", //编号
						createTime: "", //创建时间
						lastUpdateTime: "", //修改时间
						parentId: "", //上级ID
						workDate: "", //工作时间
						companyName: "", //工作单位
						department: "", //部门
						job: "", //职务
						content: "", //工作内容
					},
				],
			},
			rules: {
				name: [
					{ required: true, message: "请输入姓名", trigger: "blur" },
				],
				sex: [
					{
						required: true,
						message: "请选择性别",
						trigger: "change",
					},
				],
				birthTime: [
					{
						type: "date",
						required: true,
						message: "请输入出生年月",
						trigger: "change",
					},
				],
				identityNo: [
					{
						required: true,
						message: "请输入身份证",
						trigger: "blur",
					},
				],
				socialNo: [
					{
						required: true,
						message: "请输入社保号",
						trigger: "blur",
					},
				],
				typePolitical: [
					{
						required: true,
						message: "请输入政治面貌",
						trigger: "change",
					},
				],
				phone: [
					{
						required: true,
						validator: validatorPhone,
						trigger: "blur",
					},
				],
				nativePlace: [
					{ required: true, message: "请输入籍贯", trigger: "blur" },
				],
				education: [
					{ required: true, message: "请输入学历", trigger: "blur" },
				],
				interviewDepartment: [
					{
						required: true,
						message: "请输入面试部门",
						trigger: "blur",
					},
				],
				interviewJob: [
					{
						required: true,
						message: "请输入面试岗位",
						trigger: "blur",
					},
				],
			},
		};
	},
	methods: {
		submitForm(informationForm) {
			this.$refs[informationForm].validate((valid) => {
				let formItems = JSON.stringify(this.informationForm);

				if (valid) {
					console.log(formItems, "formItems");
					this.pagefix["page-fix"] = true;
					this.$message("验证通过");
					this.$axios({
						method: "post",
						url: "http://192.168.199.159/api/staff/v1/save",
						data: formItems,
						headers: {
							"content-type": "multipart/form-data",
						},
					}).then((res) => {
						console.log(res);
					});

					// this.$axios
					//   .post("http://192.168.199.159/api/staff/v1/save", formItems)
					//   .then((res) => {
					//     if (res.code == 200) {
					//       this.$message({
					//         type: "success",
					//         message: "保存成功!",
					//       });
					//     } else {
					//       this.$message.error("报错失败");
					//     }
					//   })
					//   .catch((error) => {
					//     this.$message.error("请检查链接");
					//   });
				}
			});
		},
		//增加删除显示控制
		isDelete(length, index) {
			if (length - 1 > index) {
				return true;
			} else {
				return false;
			}
		},
		//增加预览下载显示控制
		isPreview(length, index) {
			if (length <= 1 || length - 1 > index) {
				return true;
			} else {
				return false;
			}
		},
		handleAdd(index, rows) {
			let obj = {};
			// console.log(rows);
			//取出对象键名
			Object.keys(rows[0]).forEach((item) => {
				obj[item] = "";
			});
			rows.push(obj);
		},

		handleDelete(index, rows) {
			// console.log(index, rows, "index, rows");
			rows.splice(index, 1);
		},
		handlePreview() {},

		handleDownload() {},

		resetForm(informationForm) {
			let step = 0;
			this.$refs[informationForm].resetFields();
			this.pagefix["page-fix"] = false; //解除固定
			// console.log(this.$refs.rightOther.scrollTop);
			clearInterval(this.timeid); //屏幕回滚
			this.timeid = setInterval(() => {
				step = Math.ceil(this.$refs.rightOther.scrollTop / 10);
				step > this.$refs.rightOther.scrollTop
					? (this.$refs.rightOther.scrollTop = 0)
					: (this.$refs.rightOther.scrollTop -= step);
				//清除定时器
				if (this.$refs.rightOther.scrollTop <= 0) {
					clearInterval(this.timeid);
				}
			}, 25);
			// scrollTo(0, 0);
		},

		beforeAvatarUpload(file) {
			// console.log(file);
			const isJPG = file.type === "image/jpeg";
			if (!isJPG) {
				this.$message.error("上传头像图片只能是 JPG 格式!");
			}
			return isJPG;
		},
		uploadImage(file, fileList) {
			// console.log(file);
			this.$refs.upload.submit();
			this.imageUrl = file.url;
			if (0) {
				let fd = new FormData();
				fd.append("file", file.raw); //传给后台接收的名字 file
				this.$axios
					.post("", fd, {
						headers: { "Content-Type": "multipart/form-data" },
					})
					.then((response) => {
						//上传成功后返回的数据,
						console.log("上传图片到:" + response.data);
						// 将图片地址给到表单.
						this.informationForm.photo = response.data;
					});
			}
		},
	},
};
</script>


<style scoped lang="scss">
.formbuilder {
	width: 90%;
	min-height: 100vh;
	margin: 0 auto;

	::-webkit-scrollbar {
		/* chrome */
		display: none;
	}

	.smallTitle p:first-child {
		font-size: 12px;
	}

	.smallTitle p:nth-child(2) {
		font-size: 16px;
	}

	.el-form {
		display: flex;
		justify-content: space-between;
		width: 100%;
		height: 100%;

		.left-basic {
			width: 45%;
		}

		.right-other {
			width: 45%;
			padding: 40px 0;
			height: 800px;
			overflow: auto;
			// overflow: hidden;
			::-webkit-scrollbar {
				/*隐藏滚轮*/
				display: none;
			}
		}
		.page-fix {
			overflow: hidden;
		}
	}

	.title {
		margin-bottom: 10px;
		font-size: 16px;
	}

	.avatar-uploader .el-upload {
		position: relative;
		border: 1px dashed #d9d9d9;
		border-radius: 6px;
		cursor: pointer;
		overflow: hidden;
	}

	.avatar-uploader .el-upload:hover {
		border-color: #409eff;
	}

	.avatar-uploader-icon {
		font-size: 28px;
		color: #8c939d;
		width: 178px;
		height: 178px;
		line-height: 178px;
		text-align: center;
	}

	.avatar {
		margin-left: 35px;
		width: 100px;
		height: 142px;
		border: 1px solid #8c939d;
		display: block;
	}
}
</style>

<style lang="scss">
.inputClass {
	.el-form-item--mini.el-form-item,
	.el-form-item--small.el-form-item-form-item {
		margin-bottom: 0;
	}
	.el-input__inner {
		border: none !important;
	}
}
.el-upload--picture-card {
	border: none !important;
	line-height: 50px !important;
	height: 40px !important;
	margin-left: 10px;
}
</style>
