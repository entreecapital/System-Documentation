# Edit widgets

const express = require('express');

const router = express.Router();

const Liana = require('forest-express-sequelize');

const models = require('../../models');

const STATUS\_OPTION\_DEFAULT = 'Being processed';

const STATUS\_TRANSITIONS = {

'Being processed': \['Ready for shipping'],

'Ready for shipping': \['In transit'],

'In transit': \['Shipped', 'Failed'],

router.get('/orders/shippingStatusOptions', Liana.ensureAuthenticated, async (req, res) => {

const { context } = req.query;

const recordId = context && context.record && context.record.id;

let data = \[STATUS\_OPTION\_DEFAULT];

const order = await models.orders.findById(recordId);

const currentShippingStatus = order.shippingStatus;

if (STATUS\_TRANSITIONS\[currentShippingStatus]) {

data = STATUS\_TRANSITIONS\[currentShippingStatus];
